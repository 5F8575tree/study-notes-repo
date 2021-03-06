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

We've now seen exactly how Redux itself works by building our own imitation library. But of course, in a real
project you will use the Redux library.

**NOTE** combineReducers is a function that takes an object of reducers and returns a single reducer. Think of it as
a root reducer.

You can essentially end up with a number of further 'root'-esque reducers in much the same way that you would use
components in React. This may then give you a real root reducer file that just looks like this:

    import { combineReducers } from 'redux';
    import booksReducer from './books_reducer';
    import userReducer from './user_reducer';

    const rootReducer = combineReducers({
        books: booksReducer,
        users: userReducer
    });

    export default rootReducer;

# Redux Middleware

For an extra piece of functionality, we can add a function that checks the user's input for 'forbidden fruit'. If they enter a todo that contains a word that is something we do _not_ want them to do, we can intervene:

    function checkAndDispatch(store, action) {
        if (
          action.type === ADD_TODO &&
          action.todo.name.toLowerCase().includes("bitcoin")
        ) {
          return alert("No, that's a bad idea");
        }
        if (
          action.type === ADD_GOAL &&
          action.goal.name.toLowerCase().includes("bitcoin")
        ) {
          return alert("No, that's a bad idea");
        }
        store.dispatch(action);
      }

Now we can go through our code and anywhere we see the invocation of store.dispatch, we can replace it with checkAndDispatch and pass in the store and action. Thus, the addTodo function becomes:

    function addTodo() {
        const input = document.getElementById("todo-input");
        const name = input.value;
        input.value = "";

        checkAndDispatch(store,
          addTodoAction({
            name,
            id: generateId(),
            completed: false,
          })
        );
      }

Of course, this is not a serious idea in hardcoding 'bitcoin', but the principle and functionality itself is incredibly important as we can use this to intercept actions that we don't want to allow (emails without @ sign, for example, or non-matching passwords).

In fact, we don't need to do this ourselves, we can use Redux's built-in middleware.

## Native Redux Middleware

Middleware is '???a third-party extension point between dispatching an action, and the moment it reaches the reducer.'

What's great about middleware is that once it receives the action, it can carry out a number of operations, including:

- Producing a side effect (e.g., logging information about the store)
- Processing the action itself (e.g., making an asynchronous HTTP request)
- Redirecting the action (e.g., to another piece of middleware)
- Dispatching supplementary actions

???or even some combination of the above! Middleware can do any of these before passing the action along to the reducer.

### Checker

We can add some (slightly awkward looking) Redux middleware to replace our use of checkAndDispatch:

    const checker = (store) => (next) => (action) => {
        if (
          action.type === ADD_TODO &&
          action.todo.name.toLowerCase().includes("bitcoin")
        ) {
          return alert("No, that's a bad idea");
        }
        if (
          action.type === ADD_GOAL &&
          action.goal.name.toLowerCase().includes("bitcoin")
        ) {
          return alert("No, that's a bad idea");
        }
        return next(action);
      };

Next refers to the following piece of middleware if we have one in line _or_ it will be store.dispatch. Note that it is called **twice** in the checker function. Again, we now need to replace our checkAndDispatch calls back to store.dispatch:

    function addTodo() {

        ...

        store.dispatch(
          addTodoAction({
            name,

        ...

      }

Then we can alter our store function to include the checker middleware by passing it as the second argument:

    const store = Redux.createStore(
        Redux.combineReducers({
            todos,
            goals,
        }),
        Redux.applyMiddleware(checker)
        );

### Logger

The benefits of this logger() middleware function are huge while developing the application. We'll use this
middleware to intercept all dispatch calls and log out what the action is that's being dispatched and what the state
changes to after the reducer has run. Being able to see this kind of information will be immensely helpful while
we're developing our app. We can use this info to help us know what's going on in our app and to help us track down
any pesky bugs that creep in.

First, we can create the following function:

    const logger = (store) => (next) => (action) => {
        console.group(action.type);
        console.log("The action: ", action);
        const result = next(action);
        console.log("The new state: ", store.getState());
        console.groupEnd();
        return result;
      };

The console.group & console.groupEnd functions are used to group together similar actions and log everything that occurs in between them.

The result variable is used to dispatch the action.

Next we simply update our applyMiddleware method call within our store function to include the logger middleware:

    Redux.applyMiddleware(checker, logger);

This is truly invaluable middleware when developing web applications.

# Redux with React

It is not only React that can be linked up to Redux, you can also use Vue, Angular, html, or even plain old JavaScript. For the current purposes, however, we'll now look at how to use Redux with React.

## React as the UI

Until now we have used React within html to render our UI. But instead, we want to use React as the UI. First, we will need to add scripts for react, react-dom, and babel to our index.html file:

    <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone@7.17.6/babel.min.js"></script>

For current purposes, we will first run both the html and the react files concurrently before moving over entirely to React. First we can divide our index.html file into two parts, and add a div that will hold our React component:

    ...

       <ul id="goal-list"></ul>
    </div>

    <hr />

    <div id="app"></div>

    <script type="text/javascript">

    ...

Below our current script in the body containing the Redux codes, we will begin to connect to react with a component:

    <script type="text/babel">
      const List = (props) => {
        <ul>
          <li>List</li>
        </ul>;
      };
    </script>

We also want to render a parent component of that list component (and do this twice, once for todos and once for goals):

    const Todos = () => {
        <div>
          TODOS
          <List />
        </div>;
      };

Finally we can render both of these components within a parent component of App and render it with react-dom:

    const App = () => {
        <div>
          <Todos />
          <Goals />
        </div>;
      };

    ReactDOM.render(<App />, document.getElementById("app"));

So now we have converting a portion of our page from being rendered by the html to being rendered by React.

## Dispatching - Important!!

We now want to give our React 'App' component access to the original store that we created, and we can do this by passing it as a prop to the App component:

    ReactDOM.render(<App store={store} />, document.getElementById("app"));

**NOTE** Make sure to also pass props as a parameter in the App component itself, and down into the Todos component:

    const App = (props) => {
        <div>
          <Todos store={props.store} />
          <Goals />
        </div>;
      };

Next we want to allow the App component to accept user input. We will want to use an input ref as a part of this process. We want to pass in props to allow the Todos component to access the store. We also want to set up our button to run an event listenered that we will build called 'addItem'. We want the event handler to save the name of the input/Todo, and then subsequently set it back to an empty string. Finally, we want to let the store know that the user has added a single Todo item, and invoke our action creator 'addTodoAction'. The action creator will take in a single object, with three properties.

    const Todos = (props) => {
        const inputRef = React.useRef();
        const addItem = (event) => {
          event.preventDefault();
          const name = inputRef.current.value;
          inputRef.current.value = "";

          props.store.dispatch(
            addTodoAction({
              name,
              id: generateId(),
              completed: false,
            })
          );
        };

        <div>
          <h1>Todos List</h1>
          <input type="text" placeholder="Enter a Todo" ref={inputRef} />
          <button onClick={addItem}>Add Todo</button>
          <List />
        </div>;
      };

For simplicity, this uses the ref hook, but you will want to check this [documentation](https://reactjs.org/docs/refs-and-the-dom.html) to see whether it is necessary in your own projects.

Although as our current set up stands the html and the React sections of our app are both working from the same store, we now have a basic replication of our initial html app in React app style.

### Force Load App

We can leverage the useEffect hook in order to re-render our UI without the need to add items to the DOM, since this is what we are utilising React for.

    const App = (props) => {
        const [value, setValue] = React.useState(0);

        React.useEffect(() => {
          props.store.subscribe(() => {
            setValue((value) => value + 1);
          });
        }, []);

        const { todos, goals } = props.store.getState();

        return (
        <div>
          <Todos todos={todos} store={props.store} />
          <Goals goals={goals} store={props.store} />
        </div>
        );
      };

### Lists with React

At present, our React app section renders nothing more than a static list item that says 'List', although it is set up to receive input and update the state. We can alter the static list item so that React renders the UI to reflect the state of the store.

We can work on our List component first by giving it the props:

    <List items={list.goals} />

Then we can alter the list component to render the goals/todos. Remember to also make sure that each individual list item has a new key because we are mapping over items:

    const List = (props) => {
        <ul>
          {props.items &&
            props.items.map((item) => {
              return (
                <li key={item.id}>
                  <span>{item.name}</span>
                </li>
              );
            })}
        </ul>;
      };

With our html rendered lists, we have the ability to strike a line through completed todos, and also a button to delete the todo. Now we can work on implementing that in our React app side.

First, within our todo component we will create a removeItem function that will call our removeTodoAction action creator. We will then pass in the id of the todo that we want to remove:

    const removeItem = (todo) => {
          props.store.dispatch(removeTodoAction(todo.id));
        }

Then we can render a button next to our text and pass this removeItem function to it to run onClick:

    <button onClick={() => props.remove(item)}>X</button>

We also need to ensure our List component has access to these functions, so just as we added in the items props, we need to similarly pass in the removeItem function too:

    <List remove={removeItem} items={list.todos} />

### Toggle UI with React

The last piece of functionality that remains in our html render but not our React render is the ability to toggle the UI on the todo list.

Under our removeItem function in the todo component, let's add a toggleItem function that will call our toggleTodoAction action creator. We will then pass in the id of the todo that we want to toggle:

    const toggleItem = (id) => {
          props.store.dispatch(toggleTodoAction(id));
        };

Now again we just need to pass this new function to our list component:

    <List toggle={toggleItem} remove={removeItem} items={list.todos} />

Finally we will want to add some extra functionality to our span element in the List component, i.e. the ability onClick to style the text:

    <span
        style={{
            textDecoration: item.completed ? "line-through" : "none",
        }}
            onClick={() => props.toggle && props.toggle(item.id)}
        >
            {item.name}
    </span>

This above onClick is asking first if toggle is available and, if yes, then toggle the item via it's id (since our toggle function takes an id as an argument). The style addition gives us the option of text decoration being either line-through or none, depending on whether the items state is complete or not.

## Remove the html Rendering!

Finally our app is working as expected with both html rendering at the top and React rendering at the bottom. Since we only want one app, and we want to use React, we can now get rid of all the html rendering and rely instead on just the React JS rendering.

# Asynchronous Redux

We don't want to hold the data locally, we want to move it to an external API

## External Data

### Using a Remote API

In the real world, you wouldn't want all your data just sitting on the front end. For one, it doesn't persist. For now, we can use a fake API script added to the head of our file:

    <script src="https://tylermcginnis.com/goals-todos-api/index.js"></script>

This fake API will allow us to make asynchronous calls and get hardcoded data from our 'server', as a way to test our app.

To start, we can make a Promise call to the API to get the current state of our goals and todos. Promise.all will wait for all of the promises to resolve before moving on (so that the user doesn't need to wait a long time). Within our App component after setting our useState, we can use the following useEffect:

    React.useEffect(() => {
          Promise.all([
            API.fetchTodos(),
            API.fetchGoals().then(([todos, goals]) => {
              props.store.dispatch(receiveTodosAction(todos, goals));
            }),

            store.subscribe(() => setValue((value) => value + 1)),
          ]);
        }, []);

We can also make a new action creator that we can call receiveDataAction that will take in the data that we want to store in our store. We can then use this action creator in our useEffect:

    function receiveDataAction(todos, goals) {
        return {
          type: "RECEIVE_DATA",
          todos,
          goals,
        }
      }

This will require a new const called RECEIVE_DATA: const RECEIVE_DATA = "RECEIVE_DATA";

Then we will want to insert this variable into our separate todos and goals reducers:

    case RECEIVE_DATA:
            return action.todos;

### Loading States

Since our app fetches the data but waits for about 2 seconds to do so, we have applied a poor UX to our app. To mitigate this a little we can use a loading state to tell the user that the app is loading.

We will create a new reduce called loading:

    function loading (state = true, action) {
        switch (action.type) {
          case RECEIVE_DATA:
            return false;
          default:
            return state;
        }
      }

Now we need to again let our store aware of this new loading reducer:

    const store = Redux.createStore(
        Redux.combineReducers({
          todos,
          goals,
          loading,
        }),
        Redux.applyMiddleware(checker, logger)
      );

In our App component we also want to grab the loading state from the store:

    const { todos, goals, loading } = store.getState();

        if (loading === true) {
          return <h3>Loading...</h3>;
        }

This now means that as the data is loading, we will display a loading message, thus providing a slightly improved user experience.

### Optimistic Updates

This is an invaluable technique in UX. It basically assumes that an action will occur and then, if for some reason the API returns an error, the error will show. But otherwise, the action will be completed and the state updated without the user thinking it has not been instant!

First we will need to alter our Todos component so that the item actually gets deleted from the database (this takes a moment, so that's why we add the error alert if it fails, and if it doesn't fail we just remove the item from the list preemptively):

    const removeItem = (todo) => {
          props.store.dispatch(removeTodoAction(todo.id));
          return API.deleteTodo(todo.id).catch(() => {
            props.store.dispatch(addTodoAction(todo));
            alert ("Error deleting todo. Try again.");
          });
          };
        };

This is an **incredibly import technique** in obtaining good UX as the user gains immediate feedback, while we still get our ability to update the API state.

### Persisting Data

We need new goals or todos to persist in our API. For that, we will need to alter the addItem reducer:

        ... e.preventDefault();

          return API.saveTodo(inputRef.current.value)
            .then((todo) => {
              props.store.dispatch(addTodoAction(todo));
              inputRef.current.value = "";
            })
            .catch(() => {
              alert("Something went wrong. Try again.");
            });
        };

        const removeItem = (todo) => { ...

## Thunk

Our app now works as we want it to, but there are some issues. We currently have our data-fetching logic mixed up with our UI updating logic. We want to clearly separate these two parts. It would be preferable to build an action creator that is responsible for fetching the data, and then simply call that action creator from our UI components.

### Adding Thunk Library

We can start by making a new action creator and call it 'handleDeleteTodo, but first let's alter our removeItem function within our components to make it far more readable:

    const removeItem = (todo) => {
          props.store.dispatch(handleDeleteTodo(todo));
        };

Now we can move all of the API logic into a new action creator called handleDeleteTodo:

    function handleDeleteTodo(todo) {
        return (dispatch) => {
          dispatch(removeTodoAction(todo.id));

          return API.deleteTodo(todo.id).catch(() => {
            props.store.dispatch(addTodoAction(todo));
            alert("An error occurred");
          });
        };
      }

There is a library called 'redux-thunk' that will allow us to use thunks without having to make custom thunks, you just need to add the following script to your head:

    <script src="https://unpkg.com/redux-thunk@2.2.0/dist/redux-thunk.min.js"></script>

And again, every time we add new middleware, we need to make certain that Redux is aware that we have created it:

    Redux.applyMiddleware(ReduxThunk.default, checker, logger)

**NOTE** The placement of the middleware as arguments in the Redux.applyMiddleware function is important. It is the order in which the middleware will be executed.

Thunk middleware can then be used to delay an action dispatch, or to dispatch only if a certain condition is met (e.g., a request is resolved). This logic lives inside _action creators_ rather than inside _components_.

If a web application requires interaction with a server, applying middleware such as thunk helps solve the issue of asynchronous data flow. Thunk middleware allows us to write action creators that return functions rather than objects.

By calling our API in an action creator, we make the action creator responsible for fetching the data it needs to create the action. Since we move the data-fetching code to action creators, we build a cleaner separation between our UI logic and our data-fetching logic. As a result, thunks can then be used to delay an action dispatch, or to dispatch only if a certain condition is met (e.g., a request is resolved).

### Thunkify Initial Data

Once you have worked through and separated all the UI rendering functions/components from the API fetching logic by moving them to action creators, the app should still be working as expected. However, we want to do the same process for where our app initially gains data from the API. This is the useEffect call towards the top of the App component itself. Essentially, we want to remove the code block that starts with Promise, so that we are left with something like this:

    React.useEffect(() => {
          props.store.dispatch(handleInitialData());

          store.subscribe(() => setValue((value) => value + 1));
        }, []);

Then, of course, we need to create that handleInitialData action creator:

    function handleInitialData() {
        return (dispatch) => {
          Promise.all([API.fetchTodos(), API.fetchGoals()]).then(
            ([todos, goals]) => {
              dispatch(receiveDataAction(todos, goals));
            }
          );
        };
      }

We have now successfully separated our UI logic from our data-fetching logic.

### Advanced Asynchronous Redux

For small enough projects this process of thunking is absolutely fine, but if you get more advanced in your use of Redux and want to scale projects, you will want to consider some other options, potentially. Here are some further reading documentations that you can refer to:

    - [Github for Redux Promise](https://github.com/redux-utilities/redux-promise)
    - [Github for Redux Saga](https://github.com/redux-saga/redux-saga)
    - [Calling an API via Redux Saga Stack Overflow Thread](https://stackoverflow.com/questions/38791974/asynchronous-api-calls-with-redux-saga)
    - [Redux Promise versus Redux Saga Medium Article](https://medium.com/@shoshanarosenfield/redux-thunk-vs-redux-saga-93fe82878b2d)

# React-Redux Bindings

React and Redux are not a monogamous pair - you can use Redux to handle state for any UI rendering framework, including Angular or Vue. What we have done so far is essentially use Redux to manage our store, and then pass our store down through each React component we build in order to allow for manipulation of the store.

In short, the whole goal of binding Redux to React is to make three key aspects run as seemlessly as possible'

1. Getting state
2. Updating state
3. Listening for changes

Accessing the store is therefore very important for our components. For a small project, passing store down as props through components is not so bad, but this would be tedious and error prone in larger projects. In fact, having a store in the first place is to avoid having to pass props down through multiple components.

## Context

If you think of a situation where you are holding data towards the top of your component tree, you may have passed that data as props down through multiple child components to get to it's final destination component, even though the children that it passed through did not require it.

**Context** allows us to pass props directly to the final destination component without needing to pass it through multiple child components that don't require it.

To set it up, we first want to create a variable called 'context', and point that to the result of calling React.context:

    const Context = React.createContext();

The context variable will have two properties on it: a provider property and a consumer property.

### Context.Provider

For the component that you are rendering in App, you will want to wrap it in Context.provider (in much the same way that you would wrap in routes, etc.) For example:

    const App () => {
        return (
            <Context.Provider value={valueName}>
                <ParentComponent />
            </Context.Provider>
            );
        )
    }

### Context.Consumer

Now, for access to that prop, all we need to do is wrap the return value of our final destination component in Context.Consumer, and within that we pass in a function with the value that we want to consume as the argument. For example:

    const GrandChild () => {
        return (
            <Context.Consumer>
                {(valueName) => {
                    return (
                        <div>
                            <h1>GrandChild</h1>
                            <p>This is {valueName}</p>
                        </div>
                    );
                }}
            </Context.Consumer>
        );
    }

#### Our Todo App

In the app we have been building we have a slightly different nuance of the same problem. Rather than passing a value, such as 'name', all the way down to a deeply nested component, we are still using 'store' as props to be relied on by each component.

Here we can create a custom Provider to show what it does. The Provider renders whatever it's children are, and passes down whatever values we want to make available to any child component, in this case, access to the store:

    const Context = React.createContext();

      const Provider = (props) => {
        return (
          <Context.Provider value={props.store}>
            {props.children}
          </Context.Provider>
        );
      };

Now we need to remember to wrap the Provider component around our rendering of the App component (**Note** we no longer have the store being passed with the App component, but instead with the Provider component):

        ...

        ReactDOM.render(
            <Provider store={store}>
            <App />
            </Provider>,
            document.getElementById("app")
        );
        </script>
      </body>
    </html>

Now, any time we want to grab data from the store (get, update, listen for changes) / dispatch, we can access the store through the Provider component.

## Container Component

Also known as a 'Connected Component', because it is connected to the store. The distinction is that it is responsible for interacting with everything that is in the store, whereas other components are referred to as 'Presentational Componenents', since they are responsible for rendering UI.

In other words, the connected component will go to the store and grab the data that it needs and then passes the data as props to the presentational components to be rendered. It is a distinction between a 'worker' and a 'looker'.

This is a major benefit for **separation of concerns**.

Here is an example for connecting our App to the store:

    const ConnectedApp = () => {
        <Context.Consumer>
          {(store) => {
            return <App store={store} />;
          }}
        </Context.Consumer>;
      };

For our Goals component, the alteration would look like this:

    const ConnectedGoals = () => {
        return (
          <Context.Consumer>
            {(store) => {
              const { goals } = store.getState();

              return <Goals goals={goals} dispatch={store.dispatch} />;
            }}
          </Context.Consumer>
        );
      };

And we can now remove 'store' and turn the dispatches into props.dispatch, as well as remove the goals property from the App component. Finally, we no longer need to render Goals with props in the App component, but can instead render ConnectedGoals:

    return (
          <div>
            <Todos todos={todos} store={props.store} />
            <ConnectedGoals />
          </div>
        );
      };

You can now do the same for ConnectedTodos.

## Connecting Components

The above steps have allowed us to use a provider component that is responsible for the setting the store on to the context. In practise, any child component that requires the store can just grab it by using our Context.Consumer tags. However, this means you still need to grab Context.Consumer everytime you want to access the store. We can improve this by instead building out a connecting component (much like we built out a provider component).

Our Connect Component with need to do two things in our case: render a component, and secondly, pass the data needed from the store.

We can do this with currying (basically when the invocation is made, it invokes a further function with a second set of arguments). In our case, we need to pass our App component, and the data the connect function needs to invoke is the loading props from the store:

    const ConnectedApp = connect(((state) => {
        loading: state.loading
      }))(App);

Now within our App component we can remove the loading variable. Also, for our if statement we will need to add props.loading instead of previous where we just invoked the (now deleted) loading variable.

After making the changes to ConnectedGoals and ConnectedTodos, we now need to actually build out our abstracted connect function itself. It's quite an epic function:

        function connect(mapStateToProps) {
        return (Component) => {
          const Receiver = (props) => {
            const [value, setValue] = React.useState(0);

            React.useEffect(() => {
              let unmounted = false;
              const { subscribe } = props.store;

              const unsubscribe = subscribe(() => {
                setValue((value) => value + 1);
              });

              return () => {
                unsubscribe();
                unmounted = true;
              };
            }, []);

            const { dispatch, getState } = props.store;
            const state = getState();
            const stateNeeded = mapStateToProps(state);

            return <Component {...stateNeeded} dispatch={dispatch} />;
          };

          const ConnectedComponent = () => {
            return (
              <Context.Consumer>
                {(store) => <Receiver store={store} />}
              </Context.Consumer>
            );
          };

          return ConnectedComponent;
        };
      }

Fortunately, you don't need to remember all these steps, since this is again such a common pattern that there is a React-Redux library that carries out the functionality, by adding this script to the head:

  <script src="https://unpkg.com/react-redux@7.2.6/dist/react-redux.min.js"></script>

This is the official recommended library for using React-Redux bindings.

**NOTE** mapStateToProps is a function that lets connect() know how to map state into the component???s list of props. It is invoked with the store???s state and returns an object of props to pass to the component.

We can delete all the above parts (Context, Provider, and connect function). We need to leave ConnectedApp, ConnectedTodos and ConnectedGoals. For each of these 'Connected' functions, we will make a slight change by adding in ReactRedux to provide the connect function:

      const ConnectedApp = ReactRedux.connect((state) => ({
        loading: state.loading,
      }))(App);

Then at the very bottom, since we no longer have our own Provider function, we can likewise draw on ReactRedux for the Provider:

      ReactDOM.render(
            <ReactRedux.Provider store={store}>
              <ConnectedApp />
            </ReactRedux.Provider>,
            document.getElementById("app")
          );

#### Summary

React often leverages Redux for more predictable state management via the react-redux bindings. These bindings give us an API that simplifies the most common interactions between React and Redux.

Provider makes it possible for Redux to pass data from the store to any React components that need it. It uses React???s Context feature to make this work.

connect() connects a React component to the Redux store. The mapStateToProps() function allows us to specify which state from the store you want passed to your React component, while the mapDispatchToProps() function allows us to bind dispatch to action creators before they ever hit the component.

# Folder Structure

Of course, you don't want all your code in one file outside of learning purposes. We can instead use create-react-app and divide our code in to a more useful file structure.

    npx create-react-app todo-app

If you are starting in a fresh directory, you will also need to reinstall the following libraries:

    npm i goals-todo-api react-redux react-thunk redux

You can build a source file structure like this:

src
????????? actions # Constants, Action Creators, Asynchronous Action Creators.
??? ????????? todos.js
??? ????????? goals.js
??? ????????? shared.js
???
????????? reducers
??? ????????? todos.js
??? ????????? goals.js
??? ????????? loading.js
??? ????????? index.js # We will use this to combine all three reducers via combining reducers from Redux
???
????????? middleware
??? ????????? index.js # We will use this to combine all three middleware via combining middleware from Redux
??? ????????? logger.js
??? ????????? checker.js
???
????????? components
??? ????????? App.js
??? ????????? Todos.js
??? ????????? Goals.js
??? ????????? List.js

**RAILS-STYLE** We've organized the individual elements of our app with a "Rails-style" approach. That is, assets are grouped by "type" or "capability": any action will be found in the Actions folder, any reducer will be found in Reducers, and so on.

**Under this directory structure, if we wanted to import all actions into a component, we can get them all in a single import!**

# React Redux Project

We will complete an entire project together through these steps:

1. Project overview
2. Views and Components
3. Events
4. The Store
5. Actions
6. Middleware
7. Handling data
8. Dashboard
9. Handling Tweets
10. React Router

# Jest

Jest was developed by Facebook(Meta). You can use it to test code in React, TypeScript, Babel, Node, Vue and Angular, among others.

Alternatives: Mocha, Jasmine.

This is the basic architecture of Jest:

![Jest Architecture Example](images/jest-architecture.png)

Installation:

    npm i -D jest

Then update your package.json to include `scripts.test: jest`

To run a test:

      npm run test

Imagine a basic function in a file called _multipy.js_ that muliples two numbers:

    function multiply(a, b) {
      return a * b;
    }

    module.exports = multiply;

Our test file will be called _multipy.test.js_ and will look like this:

    var multiply = require('./multipy');

    describe('multiply', () => {
        it('will return the product of both numbers passed', () => {
            expect(multiply(2, 3)).toEqual(6);
        });
    })

## Jest Matchers

Jest matchers are used to compare two values: expected, and actual.

### expect() Matcher

Allows you to check the value passed to it against a certain condition.

#### toEqual()

Verifies that the value of an object is equal to what you _expect()_

    expect(multiply(2, 3)).toEqual(6);

Returns true to pass the test.

#### toBeLessThan()

Expected number will be smaller than the actual number.

    expect(2).toBeLessThan(3);

#### toBeLessThanOrEqual()

    expect(2).toBeLessThanOrEqual(2);

#### toBeGreaterThanOrEqual()

    expect(3).toBeGreaterThanOrEqual(2);

#### toBeGreaterThan()

    expect(3).toBeGreaterThan(2);

### not() Matcher

Useful if you have updated a number and you want to test that is no longer matches the original value.

    expect(multiply(2, 3)).not.toEqual(5);

    expect(5).not.toBeLessThan(1);

Here is a list of [Jest's expect() Matchers.](https://jestjs.io/docs/expect)

### String Matchers

#### toMatch()

    expect('Hello World').toMatch(/Hello/);

Return true is the regex substring /Hello/ is found in the string.

#### toContain()

Verify if an array contains a specific object.

    expect([1, 2, 3, 4]).toContain(3);

    expect(["cat", "dog", "bird"]).toContain("dog");

Both return true and pass the test.

### Null Matcher

Returns true if a value is null.

    let test = null;

    expect(test).toBeNull();

### Exception Matcher

#### toThrow()

Verify that the function we are passing to it throws an exception.

    function throwAnError(text) {
        throw new Error('Error: ' + text);
    }

    expect(throwAnError('myError')).toThrow();

## Creating a Test File

We have a function called filterArray. The function expects an array of numbers to be passed to it. If the array is null, the function returns null. If not, the function maps over the array and returns all numbers, except where a number is higher than 100, in which case it returns that number as 100.

    function filterArray(numbers) {
        if (numbers  === null) {
            return null;
        }
        return numbers?.map(n => n > 100 ? 100 : n);
    }

    module.exports = filterArray;

We need to test for three features:

1. Null is returned if the array is null.
2. If an array of 4 numbers is passed, the function returns an array of 4 numbers (and match the numbers).
3. If a number bigger than 100 is passed, it is altered to 100.

Here is a solution to run three tests on our function:

    var filterArray = require('./filterArray');

    describe('filterArray', () => {
        it('will return null if null is passed', () => {
            var results = filterArray(null);
            expect(results).toBeNull();
        });

        it('will return all numbers lower than 100', () => {
            var mockArray = [1, 2, 3, 4];
            var results = filterArray(mockArray);
            expect(results.length).toEqual(mockArray.length);
            expect(results[0]).toEqual(mockArray[0]);
            expect(results[1]).toEqual(mockArray[1]);
            expect(results[2]).toEqual(mockArray[2]);
            expect(results[3]).toEqual(mockArray[3]);
        });

        it('will not return any numbers greater than 100.', () => {
            var mockArray = [50, 75, 100, 125];
            var results = filterArray(mockArray);
            expect(results).not.toContain(125);
        });
    });

**NOTE**: Our function works correctly where not.toContain(125) returns true, since the function is intended to change 125 to 100.

## Asynchronous Jest

Asynchronous functions depend on an event that is outside of our code. Most often, this is for performing CRUD operations with server-side code, and awaiting a response.

When testing asynchronous functions, we need to let Jest know that we are awaiting a response. We can do this by using async/await within our test. For example, if we have the following function to test (_note_ we have added a 2 second timeout to simulate an API call):

    // isUtensilAvailable.js

    var utensils = ['fork', 'knife', 'spoon'];

    function isUtensilAvailable(utensil){
        return new Promise((resolve, reject) => {
            setTimeout(() => {
            utensils.includes(utensil)
                ? resolve(true)
                : reject('No utensils found.')
            }, 2000);
        });
    }

    module.exports = isUtensilAvailable;

We can simply add async and await at the correct places in our test code. I.e. adding async before the function, and await after the function and before the expect() statement:

    // isUtensilAvailable.test.js

    var isUtensilAvailable = require('./isUtensilAvailable');

    describe('isUtensilAvailable', () => {
        it('will return true if the utensil is found', **async**() => {
            var utensil = 'fork';
            var result = **await** isUtensilAvailable(utensil);
            expect(result).toEqual(true);
        });

        it('will return an error if the utensil is not found', **async**() => {
            var invalidUtensil = 'tree';
            **await** expect(isUtensilAvailable(invalidUtensil)).rejects.toEqual('No utensils found.');
        });
    })

There are two tests here, one that checks the code when the utensil is found, and one that checks the code when the utensil is not found.

## React Testing Library

A JavaScript testing utility created specifically for rendering and testing React Components. You use it in conjunction with Jest to write tests for React components.

The website for [React-Testing-Library](https://testing-library.com/) is really useful.

    npm install --save-dev @testing-library/react @testing-library/jest-dom

After installation, an App.test.js file is automatically built and added to you files.

screen.debug() can be used to test the rendering of the App component and will print in the terminal the HTML output of the component. In this case the test passes automatically, of course, since we have yet to enter any testing.

## Snapshot Testing

A snapshot test allows you to verify that a component renders the way you expected. The first time you run the test, a **snapshot** file is created. Then on subsequent tests you can compare the current output to the snapshot file - is the new snapshot matches the first snapshot, the test passes. Otherwise, the test fails.

To run a snapshot test, you simply need to run the test to expect:

    expect(component).toMatchSnapshot();

Snapshot tests are very useful for testing components that you do not expect to change frequently. For example, if you made a change in the code that is not intended to be cosmetic, i.e. you expect the UI to remain the same, a snapshot test can be of great use.

There are two ways to update a snapshot if you want to actually change the UI. You can either delete the original snapshot file, causing the test to run as though it is the first time. Or, when the test fails, you have the option of typing 'u' in the console to update the snapshot file.

## React DOM Testing

### Querying Elements

There are four major query methods that we will look at:

1. getBy
2. queryBy
3. getAllBy
4. queryAllBy

When we know we have a particular element in the DOM, we can use the getBy test, in which if there is no such element found, an error is returned and, likewise, if _more than one_ such element is found we also get an error. In other words, getBy seeks just one element in the DOM that matches the test parameter.

queryBy can be useful for edge cases where we know we want an element to exist in certain cases, but not in other cases. If no matches are found, null is returned, allowing the test to continue. An error is only thrown if multiple matches are found.

Both getAllBy and queryAllBy are similar, but instead search for _all_ such elements in the DOM.

#### When to get and when to query?

As a rule-of-thumb, use get when you want your test to verify if an **element is present**.

Use query when you want to search and verify that an element is **not present**.

#### Selecting Elements: what _get_ or _query_ by?

The two major searches are for **text/regex** and **TestId**.

For example, if the follow is used, the test will run to try and retrieve one element that contains the text 'Hello':

    getByText(/Hello/);

For multiple elements:

    getAllByText('Column');

For TestId, we can search for a specific HTML tag. For example:

    getByTestId('submit-button');

Of course, you need the element to contain the data-testid="submit-button" attribute.

Bringing all these elements together to test an App component, we can produce a text like this:

    import { render } from '@testing-library/react';
    import * as React from 'react';
    import App from './App';

    describe('App', () => {
        it('will have all expected fields', () => {
            var component = render(<App />);

            var labels = component.getAllByText(/name/)
            expect(labels.length).toEqual(2);

            var firstNameInput = component.getByTestId('first-name-input')
            var lastNameInput = component.getByTestId('last-name-input')
            expect(firstNameInput).toBeInTheDocument();
            expect(lastNameInput).toBeInTheDocument();

            var submitButton = component.getByText('Submit')
            expect(submitButton).toBeInTheDocument();
        });
    })

### Firing Events

Firing events allow your Jest test to simulate an event occurring on the DOM.

fireEvent.click similates a click. fireEvent.change similates a change. fireEvent.keyDown simulates a key press, and so on.

    import * as React from 'react';
    import { render, fireEvent } from '@testing-library/react';
    import { NameForm } from './App';

    describe('NameForm', () => {
        it('will display an error if the name is not provided.', () => {
            var component = render(<NameForm />);

            var submitButton = component.getByTestId('submit-button');
            fireEvent.click(submitButton);
            expect(component.getByTestId('error-header')).toBeInTheDocument();
            expect(component.queryByTestId('success-header')).not.toBeInTheDocument();
        });

        it('will display a success message if the name is provided.', () => {
            var component = render(<NameForm />);

            var input = component.getByTestId('name-input');
            fireEvent.change(input, { target: { value: 'Mike' } });
            var submitButton = component.getByTestId('submit-button');
            fireEvent.click(submitButton);
            expect(component.getByTestId('success-header')).toBeInTheDocument();
            expect(component.queryByTestId('error-header')).not.toBeInTheDocument();
        });
    });

# Test-Driven Development

The concept of writing tests while writing your software is known as "TDD", and is often very popular among tech companies.

Book Recommendations:

**1. The Pragmatic Programmer - David Thomas and Andrew Hunt**

- This is essential reading for any programmer.

**2. Clean Code: A Handbook of Agile Software Craftmanship - Robert Martin**
