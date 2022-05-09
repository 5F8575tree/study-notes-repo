# Redux

## Table of Contents

# Managing State

## What is Redux?

Essentially, Redux aims to simplify the management of state in React apps by providing one central stroe (tree) for all states. This hopefully means you do not get lost figuring out where your state is being stored.

With Redux, you can interact with this single store to: - Get the current state - Listen for changes - Update the state. **Data will be stored outside of the app and will simply be referenced within the app - keeping things more simple and clean.**

## The State Tree

One of the best ways to improve the quality of an app you build is to improve the predictability of the state that is being managed. Most bugs are caused by state mismanagement: for example, a mobile app showing you a notification alert without a notification existing.

The sole single place where our data is stored with Redux is the state tree. This means you do not have problems with duplicate data, and also you have full control over state management through a single source object.

## The Store

Contains the state tree, as well as the actions that can be manipulated on data with reducers: getting state, updating state, and listening for changes.

You can build out the Store in an index.js file, create a factory function to store objects, keep track of state, and then you can build methods to call on the store.

# Build the Store

## Getting the State

Create an index.js file and write the following:

    function createStore() {
        let state;

        const getState = () => state;

        return {
            getState,
        };
    }

**NOTE**: currently we have a _private_ state variable, and a _public_ getState method. There are no arguments that are set up to be passed yet.

getState will simply return the current state.

## Listen to Changes

We have now got a store with the state, and we have a method to get the state. Next, we will want to add a way to listen to changes on that state.

For this can create an array and a function (called 'subscribe') which we can use to populate that array. We want to be able to take our array and then we want to push into it the function that is being passed to our subscribe function when it is invoked.

    function createStore() {

        let listeners = [];

        ...

        const subscribe = (listener) => {
            listeners.push(listener);
        };

    return {
        ...
        subscribe,
    };
    }

We've given the user the ability to subscribe to changes, but we also want them to be able to unsubscribe to changes. We can do this by returning a function to the user after they invoke subscribe. When they invoke this new, returned function, we can now filter out (internally) the original listener that was passed to the subscribe function. We can simply call this second function 'unsubscribe'.

    function createStore() {
        ...

        const subscribe = (listener) => {
            listeners.push(listener);
            return () => {
                listeners = listeners.filter((l) => l !== listener);
                };
            };

        ...

        }

## Update the State

The whole point of Redux is to increase predictability of state. Thus, **Rule #1 is: Only an event can change the state of the store**.

In short, we need a standard set of events in our application that will change the state of the store, basically like a rulebook.

**Actions** are the events that will change the state of the store. They are objects that contain a title, an id and any necessary data related to the event. For example, for a TODO list app you might have an action called 'ADD_TODO' that will add a new todo to the store:

    {
        type: 'ADD_TODO',
        todo: {
            id: 0,
            title: 'Learn React',
            completed: false,
        },
    }

You could have similar **actions** for 'REMOVE_TODO' and 'TOGGLE_TODO'. These actions are all essentially just records of state changes.

**NOTE** An action is just a simple JavaScript object, so you can add an property you like to it. Since every single action has it's own 'type' property, it will be impossible to get them confused with other actions! Great!

**Action Creators** are functions that create actions linked together. We use them to ensure that we pass as little data to each action as possible as a matter of good practise. The work as functions that return/create action objects.

For example, if we had a tour company selling tours, we may have an action such as 'ADD_TOUR_TO_CART'. It could then take other properties, such as a tour id. This would give us something like this:

    {
        type: 'ADD_TOUR_TO_CART',
        tourId: 14,
    }

An action creator would then be something like this:

    const addTour = (tour) => ({
        type: ADD_TOUR_TO_CART,
        tourId,
    });

**Rule #2 is: The function that returns the new states must be a pure function**.

#### Pure Function

Pure functions are defined by 3 characteristics:

1. They always return the same results if the same arguments are passed in.
2. They depend entirely on the arguments passed into them - they _never_ access values outside of their own scope.
3. They never produce any side effects - so no interaction with the outside world can occur, i.e. APIs.

Any example of an impure function:

    const tipPercentage = 0.15;

    const calculateTip = (cost) => cost * tipPercentage;

It is not pure since it relies on a variable, tipPercentage. It could be refactored to by pure in the following way:

    const calculateTip = (cost, tipPercentage = 0.15) => cost * tipPercentage;

Pure functions are gold because they are 100% predictable.

### Reducer Function

With all this in mind, we can now create a reducer that will update the state of the store. This will be a pure function that is responsible for updating the state in our store and simply takes the **state** as one argument and the **action** as the other. It's purpose is to take the action and return a new version of our state.

    functions todos (state = [], action) {
        if (action.type === 'ADD_TODO') {
            return state.concat([action.todo]);
        }
        return state;
    }

Since concat returns a new array, we are not altering the state, but instead returning a new array. If the action type doesn't match the one we want, we simply return the state. We add the empty array as if this is the first time the action is being called there will otherwise be no state to concat, and we would get an error. In essence we are saying 'if no state currently exists, set the initial state as an empty array'.

This is called a reducer because it is a pure function that takes a state and a function and then reduces that to a brand new state.

### Dispatching an Action

Now we have a store which holds our state, a way to get that state, and a way to listen to changes on that state. We also have a reducer that will take in the state and an action and return a new state. So now we just need the final piece: **updating the state of our store**.

We can do this with a **dispatch function**, which is responsible for updating the state within the store. To do so, it needs to receive the action that tells dispatch what event occurred within the application.

Within dispatch we can use whatever gets returned from calling the reducer function. We also want it to loop through our array of listeners that we set up so that any listenere the user set up will also be invoked.

    const dispatch = (action) => {
        state = reducer(state, action);
        listeners.forEach((listener) => listener());
    }

    ...

    return {
        ...
        dispatch,
    };

We also need to change createStore to receive the reducer (**because the reducer function is going to be a part of the application and not part of the store, which is basically library code**):

    function createStore(reducer) {
        ...
        return {
            ...
    }

Now whenever the user wants to update the state internally inside our store, they can simply call dispatch while passing it the specific action which occurred.

What is now happening:

1. dispatch() is called with the action that occurred.
2. The reducer that was passed to createStore is called with the current state tree and the action. This then updates the state interally in the store.
3. Because the state has (potentially) changed, all the listener funtioncs that have been regitered with the subscribe() methods are called.

## Putting it All Together

In the app, if we wanted to invoke what we have created with our store we can use the following:

    const store = createStore(todos);
    store.subscribe(() => console.log('The new state is', store.getState()));

    store.dispatch({
        type: 'ADD_TODO',
        todo: {
            id: 0,
            name: 'Learn Redux',
            complete: false,
        }
    });

**Now every time we want to update the state of our store, all we have to do is call dispatch (store.dispatch()) with the action that occurred.**
