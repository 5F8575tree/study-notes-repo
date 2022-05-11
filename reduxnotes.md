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

Middleware is '…a third-party extension point between dispatching an action, and the moment it reaches the reducer.'

What's great about middleware is that once it receives the action, it can carry out a number of operations, including:

- Producing a side effect (e.g., logging information about the store)
- Processing the action itself (e.g., making an asynchronous HTTP request)
- Redirecting the action (e.g., to another piece of middleware)
- Dispatching supplementary actions

…or even some combination of the above! Middleware can do any of these before passing the action along to the reducer.

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
