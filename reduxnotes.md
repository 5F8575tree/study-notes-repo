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

### Building a Todo Application

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

We also want to be able to remove a todo and toggle. For this, we need to alter our reducer function:

    function todos (state = [], action) {
        if (action.type === 'ADD_TODO') {
            return state.concat([action.todo]);
        } else if (action.type === 'REMOVE_TODO') {
            return state.filter((todo) => todo.id !== action.id);
        } else if (action.type === 'TOGGLE_TODO') {
            return state.map((todo) => todo.id !== action.id ? todo :
            Object.assign({}, todo, { complete: !todo.completed }));
        } else {
            return state;
        }
    }

**Note**: This remains a pure function as it only depends on the action and the state - we are not altering the state, just using it for concat, map, filter, and a touch of Object.assign to create a new object.

One problem with the todos function we have created is that it encompasses a lot of actions, and where you notice a lot of if statements, you may find it easier to fall back on a switch statement:

    function todos (state = [], action) {
        switch (action.type) {
            case 'ADD_TODO':
                return state.concat([action.todo]);
            case 'REMOVE_TODO':
                return state.filter((todo) => todo.id !== action.id);
            case 'TOGGLE_TODO':
                return state.map((todo) => todo.id !== action.id ? todo :
                Object.assign({}, todo, { complete: !todo.completed }));
            default:
                return state;
        }
    }

Adding was pretty clear. But to clarify, when we used REMOVE_TODO, we called filter() on the state. This returns a new state (an array) with only todo items whose id's do not match the id of the todo we want to remove. Then we added the TOGGLE_TODO case, we want to change the value of the 'complete' property on whatever id is passed along on the action. We mapped over the entire state, and if todo.id matched action.id, we used Object.assign() to return a new object with merged properties. If it didn't match, we returned the original object: (todo.id !== action.id ? todo) - where the : is the 'or' operator.

With the addition of the switch statement, we checked the action.type against the various 'case' statements and returned the appropriate state. It _feels_ a little bit cleaner this way.

### A Goal's Functionality

The app is pretty simple with just managing a todo list. We can make it a bit more interesting by managing a list of goals as well.

    function goals(state = [], action) {
        switch (action.type) {
            case "ADD_GOAL":
                return state.concat([action.goal]);
            case "REMOVE_GOAL":
                return state.filter((goal) => goal.id !== action.id);
            default:
                return state;
        }
    }

Now instead of having a single reducer, we have two reducers. This is an issue as we _cannot_ pass our createStore function two reducers. We need to create a **Root Reducer** that can act as a middleman between our separate reducers and our createStore function.

Previously both of our reducers set the state to arrays. Instead, we can create a reducer that can set the state to a list of objects:

    function app (state = {}, action) {
        return {
            todos: todos(state.todos, action),
            goals: goals(state.goals, action),
        };
    }

Now instead of passing todos to createStore, we can pass app: const store = createStore(app);

## Improving our Code

### Constants

We have placed a large number of strings in our code so far: 'ADD_TODO', 'TOGGLE_TODO', 'ADD_GOAL', etc. and strings are prone to typos. It is a good idea to create constants for these strings.

Thus, instead of the string, we can create variables at the top of our app code (not in our store):

    const ADD_TODO = 'ADD_TODO';
    const TOGGLE_TODO = 'TOGGLE_TODO';
    const ADD_GOAL = 'ADD_GOAL';
    ...

Now we avoid any misspellings or typos that wouldn't show up in any error.

### Action Creators

If we make a large number of actions in our application, we are hardcoding and duplicating a lot of code. Instead, we can create action creators. For example, with our ADD_TODO actions, we can instead use:

    function addTodoAction (todo) {
        return {
            type: ADD_TODO,
            todo,
        };
    }

And with that, we no longer need to repeat the speicific type and the potentially numerous todo objects (id, name, complete, etc.)

Now to invoke it with a dispatch we can use:

    store.dispatch(addTodoAction({
        id: 1,
        text: "Learn Redux",
        completed: false
        })
    );

For the adding actions you still need to enter quite a bit of code, but action creators really become useful where only an id is required. For example if we made a removeTodoAction and gave it the parameter (id) we can invoke it like this:

    store.dispatch(removeTodoAction(0));

This really cleans up our code.

# UI and State

## UI

We have now built the major portion of our redux project, but we now need to add some UI to complete the interaction.

### index.html

We want our code to render to a browser, so for now we can simply copy it all from index.js (and delete that file), create index.html, and then paste the code between the old-school script tags in the html file.

    < script type="text/javascript > < / script >

This of course renders only a blank page, but the console should be logging our state.

You will now want to add some basic UI so that you can test the functionality of your redux app. Remember that we have the 'library style' code, and the 'app' code. We can leave the library code within our script tags, but we will want the DOM/view to render our app code.

    <div class="todo-list">
      <h1>Todo List</h1>
      <input id="todo-input" type="text" placeholder="Enter a todo" />
      <button id="todo-button">Add Todo</button>
      <ul id="todo-list"></ul>
    </div>

Repeat the same for goals. Although not pretty, at least we have something rendered to screen.

### Hooking up the UI and State

First we need to add functions that are hooked up to our two buttons, one for Todo and one for Goals. We want to grab the value of what the user types into the input field and store it in a variable called 'name' (for example). Then we want to reset the input value to an empty string. Then we want to take the value we have stored in the 'name' variable and invoke the addTodoAction through a dispatch function. We will pass the action creator function three properties: name (which is the value of the user input), an id, and the completed status of 'false'.

    function addTodo () {
        const input = document.getElementById('todo-input');
        const name = input.value;
        input.value = '';

        store.dispatch(addTodoAction({
            name,
            id: generateId(),
            completed: false,
        }));
    }

**NOTE** We can use a helper function to generate id's for us:

    function generateId () {
        return Math.random().toString(36).substring(2) + (new Date()).getTime().toString(36);
    }

We need to do the same for our goals (but we don't use the completed property). We then need to hook these up to our two separate buttons so that when they are clicked the addTodo and addGoal functions are invoked.

    document.getElementById('todo-button').addEventListener('click', addTodo);
    document.getElementById('goal-button').addEventListener('click', addGoal);

And now the UI and state are linked up! If you head to the browser and type something into the todo input and click the button, you will notice in our console we receive 'the new state is' and a new array in our todos object.

### Update UI

We now have the ability to manipulate the state through interacting with the UI. Now we want to make it so that the browser displays the state in the UI. First we will create a function that renders the UI to the DOM, and pass it a todo argument. Then we need the function to create a brand new list node, as well as a text node which will just be the name of the todo. We will then grab the new node and append to it our text node as a child. Next we will grab our ul element and append onto it the new list node.

    function addTodoToDOM (todo) {
        const node = document.createElement('li');
        const text = document.createTextNode(todo.name);
        node.appendChild(text);

        document.getElementById('todo-list').appendChild(node);
    }

Again, we want to do something similar with our goals.

We can now remove the console.log of the new state within the store.subscribe function, and instead we can get the state and pass it to the DOM. You also _must_ reset the lists every time this function is run, however, since if you do not then you will get duplicate entries (we want to wipe the DOM each time, because we are relying on state to management what gets rendered).

    store.subscribe(() => {
        const { todos, goals } = store.getState();

        document.getElementById('todo-list').innerHTML = '';
        document.getElementById('goal-list').innerHTML = '';

        todos.forEach(addTodoToDOM);
        goals.forEach(addGoalToDOM);
    });

One last aspect we want to create is the ability to check off todos. We can do this by adding an event listener to the list items. We will add an event listener to the list items, and when the user clicks on the list item, we will toggle the completed status of the todo. In our addTodoToDOM function, we will add a style class to the list item depending on the completed status of the todo. We then want an event listener to the list items that will toggle the completed status of the todo.

    function addTodoToDOM (todo) {
        ...
        node.style.textDecoration = todo.completed ? 'line-through' : 'none';
        node.addEventListener('click', () => {
            store.dispatch(toggleTodoAction(todo.id));
        }
        ...
    }

### Removing Items

We basically have two tasks to create a remove button to get rid of an item on the todo list (or goals list). First, we can create a function that creates the button itself:

    function createRemoveButton(onClick) {
        const removeBtn = document.createElement("button");
        removeBtn.innerText = "X";
        removeBtn.addEventListener("click", onClick);
        return removeBtn;
      }

And then we need to place it alongside the text node that we create when the user inputs a new todo item, and pass in the create button function so that a button is created along with the text list element:

    function addTodoToDOM (todo) {

        ...

        const text = document.createTextNode(todo.name);

        const removeBtn = createRemoveButton(() => {
          store.dispatch(removeTodoAction(todo.id));
        });

        node.appendChild(text);
        node.appendChild(removeBtn);

        ...

    }

**NOTE** as you can see, the createRemoveButton 'contains' our dispatch action creator 'removeTodoAction', so that we can keep track of the state.

We need to repeat this for our goal section.

# Redux Library

All of the walkthrough we did above was essentially using our own custom library that works like Redux, but it wasn't Redux. Redux is a library that has a store, actions, and reducers for us!

## Adding in Redux

In the head of our application, we can now import the library with a script:

    <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/4.1.2/redux.min.js"></script>

Now we can delete the 'library' section of code we built, and also when we create our store instead of using our own custom library, we can use the Redux library. We can also delete our 'app' function (the function that was able to handle two separate state's that we wanted to manage) since Redux actually has the exact same functionality:

    const store = Redux.createStore(
        Redux.combineReducers({
          todos,
          goals,
        })
      );

We've now seen exactly how Redux itself works by building our own imitation library. But of course, in a real project you will use the Redux library.

**NOTE** combineReducers is a function that takes an object of reducers and returns a single reducer. Think of it as a root reducer.

You can essentially end up with a number of further 'root'-esque reducers in much the same way that you would use components in React. This may then give you a real root reducer file that just looks like this:

    import { combineReducers } from 'redux';
    import booksReducer from './books_reducer';
    import userReducer from './user_reducer';

    const rootReducer = combineReducers({
        books: booksReducer,
        users: userReducer
    });

    export default rootReducer;

# Redux Middleware
