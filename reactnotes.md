# 1. REACT

React is a frontend library for building user interfaces. It is used for building web applications. If you just need a standard, static website, you can stick with HTML, CSS, and JavaScript. If you need dynamic pages, you can use React.

## 1.1. MERN Stack

- **MongoDB**, which is the application’s database
- **Express**, which handles the application’s backend
- **React**, which is used to build the front end
- **Node**, which is the runtime environment for the application

## 1.2. Table of Contents

- [1. REACT](#1-react)
  - [1.1. MERN Stack](#11-mern-stack)
  - [1.2. Table of Contents](#12-table-of-contents)
- [2. Why Use React?](#2-why-use-react)
  - [2.1. Composition](#21-composition)
  - [2.2. Declarative Code](#22-declarative-code)
  - [2.3. Unidirectional Data Flow](#23-unidirectional-data-flow)
  - [2.4. React is Just JavaScript](#24-react-is-just-javascript)
  - [2.5. ES6 Syntax](#25-es6-syntax)
  - [2.6. Functional Programming](#26-functional-programming)
    - [2.6.1. Array map() Method](#261-array-map-method)
    - [2.6.2. Array filter() Method](#262-array-filter-method)
    - [2.6.3. Using filter() with map()](#263-using-filter-with-map)
  - [2.7. The Virtual DOM](#27-the-virtual-dom)
- [3. Rendering UI with React](#3-rendering-ui-with-react)
  - [3.1. Creating UI Elements](#31-creating-ui-elements)
    - [3.1.1. Props](#311-props)
    - [3.1.2. Nesting with the Third Element](#312-nesting-with-the-third-element)
  - [3.2. JSX](#32-jsx)
  - [3.3. Components in JSX](#33-components-in-jsx)
    - [3.3.1. Traditional v Arrow Function Syntax](#331-traditional-v-arrow-function-syntax)
    - [3.3.2. The 'this' Keyword](#332-the-this-keyword)
  - [3.4. create-react-app](#34-create-react-app)
  - [3.5. Composition](#35-composition)
- [4. State Management](#4-state-management)
  - [4.1. Props](#41-props)
  - [4.2. State](#42-state)
  - [4.3. How to Change State](#43-how-to-change-state)
  - [4.4. PropTypes](#44-proptypes)
  - [4.5. Controlled Components](#45-controlled-components)
- [5. React Workflow](#5-react-workflow)
- [6. Hooks](#6-hooks)
  - [6.1. What are Hooks?](#61-what-are-hooks)
  - [6.2. Side Effects](#62-side-effects)
  - [6.3. Using a Database](#63-using-a-database)
  - [6.4. Removing Data from the Database](#64-removing-data-from-the-database)
  - [6.5. Side Effect Cleanup](#65-side-effect-cleanup)
  - [6.6. Additional Hooks](#66-additional-hooks)
- [7. Routing](#7-routing)
  - [7.1. Single Page Applications](#71-single-page-applications)
  - [7.2. React Router](#72-react-router)
  - [7.3. Dynamically Rendering Pages](#73-dynamically-rendering-pages)
  - [7.4. Install React Router](#74-install-react-router)
  - [7.5. Broswer Router](#75-broswer-router)
  - [7.6. Navigation with < Link >](#76-navigation-with--link-)
  - [7.7. Navigation with < Route >](#77-navigation-with--route-)
  - [7.8. Building a Form](#78-building-a-form)
    - [7.8.1. Form Serialization](#781-form-serialization)
  - [7.9. Update Server with New Contact](#79-update-server-with-new-contact)
- [8. Learn More about React Router](#8-learn-more-about-react-router)

# 2. Why Use React?

## 2.1. Composition

We are used to using functions, and then using a single function that is composed of the other functions to return a value. In react, it works in the same way, but instead of writing functions to return some values, we compose the functions to **return UI elements.**

Composition is a way of combining **simple functions** to create more complex ones in **combination**.

This is one factor that makes React so useful. The _key difference_ between simply combining differing functions and using composition is based on the DOT idea ('Do One Thing'). In other words, with JavaScript we can combine functions to grab a user ID, build a url, and update the UI. But this is actually a 'monster' function that does three things. With React, you use composition to, for example, creating the following:

    <page>
        <article>
        <sidebar>
    </page>

This ensures that the page component actually contains the article and sidebar components.

## 2.2. Declarative Code

Another key factor in React. Much of JavaScript is imperative code. To use a metaphor: if you are driving your car and want to keep the temperature at 70 degrees, you have to manage windows, the aircon, and air flow. You can achieve 70 degrees throughout your drive, but you need to keep adjusting the three different imperatives - you are telling it exactly what to do at each step.

With React, you use **declarative** code to say 'I want the temperature to remain at 70 degrees', and it handles all of the other determinants for you.

A code example would be the use of event listeners in JavaScript, and the use of the `onClick` attribute in React. 'onClick' can be simply written and assigned a function (e.g. 'handleSubmit').

## 2.3. Unidirectional Data Flow

Angular (and Vue.js) uses two-way data bindings, which means that whether the data is updated by the model or the view, it updates the other. This can be great, but it also means that it can be hard to discern what is happening in the application.

With React, the data 'lives' in the parent component, and can be used by child components. If the child component requires an update, it sends this update to the parent component where the update is actually performed.

In the following code, for example, only the <FlightPlanner> component should be updated.

    <FlightPlanner>
        <DatePicker />
        <DestinationPicker />
    </FlightPlanner>

If a particular component is the child of two components, both parents can update the child. Thus, in the following example, both <FlightPlanner> and <LocationPicker> are responsible for updating the data in the other elements (while only <FlightPlanner> is responsible for the <DatePicker /> child).

    <FlightPlanner>

        <LocationPicker>
            <OriginPicker />
            <DestinationPicker />
        </LocationPicker>

    <DatePicker />

    </FlightPlanner>

In short, data flows in only one direction, from parent to child. If data is shared between sibling child components, then the data should be stored in the parent component and passed to both of the child components that need it.

## 2.4. React is Just JavaScript

React uses JavaScript syntax where it is easier to do so. For example, to loop through an array, you can just use .map() method that is built in to JS.

    const items = [1, 2, 3, 4, 5];
    const mappedItems = items.map(item => item * 2);

    console.log(mappedItems);

    // [2, 4, 6, 8, 10]

## 2.5. ES6 Syntax

ES6 syntax is the new standard for JavaScript. It is a superset of JavaScript, and is used in React. Thus, you can use aroow functions, let/const variables, spread syntaxt (...), using functions as variables(e.g. const myFunctionVar = myFunction() ), and other ES6 features.

## 2.6. Functional Programming

One of the greatest benefits of React is the ability to use **functional programming**. Functional programming is a programming paradigm that treats functions as first-class objects. This means that functions can be passed around, and can be returned from other functions. They can be stored in variables, and can be passed as arguments to other functions. They can also allow array methods such as map, filter, and reduce to be used on functions.

### 2.6.1. Array map() Method

JavaScript's map() method calls on an existing array and returns a new array based on what is returned from the function that's passed as an argument. **The method creates a new array, and does NOT modify the original array.**

Let's say we have an array named 'names', and we want to find the length of each name and store them in a new array:

    const nameLengths = names.map((name) => name.length);

This code will return an array of the lengths of each name in the 'names' array. The following code will loop over an album data array and return an array of strings that each say '<albumName> by <artistName> sold <albumSales> copies': -

        const musicData = [
        { artist: 'Adele', name: '25', sales: 1731000 },
        { artist: 'Drake', name: 'Views', sales: 1608000 },
        { artist: 'Beyonce', name: 'Lemonade', sales: 1554000 },
        { artist: 'Chris Stapleton', name: 'Traveller', sales: 1085000 },
        { artist: 'Pentatonix', name: 'A Pentatonix Christmas', sales: 904000 },
        { artist: 'Original Broadway Cast Recording',
        name: 'Hamilton: An American Musical', sales: 820000 },
        { artist: 'Twenty One Pilots', name: 'Blurryface', sales: 738000 },
        { artist: 'Prince', name: 'The Very Best of Prince', sales: 668000 },
        { artist: 'Rihanna', name: 'Anti', sales: 603000 },
        { artist: 'Justin Bieber', name: 'Purpose', sales: 554000 }
    ];

    const albumSalesString = musicData.map(album =>`${album.name} by ${album.artist} sold ${album.sales} copies`);

    console.log(albumSalesString);

    // [
    //     '25 by Adele sold 1731000 copies',
    //     'Views by Drake sold 1608000 copies',
    //     'Lemonade by Beyonce sold 1554000 copies',
    //     etc. etc.
    // ]

### 2.6.2. Array filter() Method

As with the map() method, this method takes an array, with the function passed as an argument, and returns a new array. The difference is that this method filters out items from the original array based on a condition.

    const shortNames = names.filter((name) => name.length < 6);

To use our musicData example:

    const results = musicData.filter(album => album.name.length >= 10 && album.name.length <= 25);

    console.log(results);

This will return 3 objects from the musicData array with an album name between 10 and 25 characters long.

### 2.6.3. Using filter() with map()

We can combine the two methods to create an array that passes through the filter() and then returns a new array of that filtered data.

    const results = musicData
                    .filter(album => album.name.length >= 10 && album.name.length <= 25)
                    .map(album => `${album.name} by ${album.artist} sold ${album.sales} copies`);

    console.log(results);

**Note:** Running filter first is faster, since both loop through the entire array their are provided with, and so the filtered array will be less work that the mapped array.

Here is an example with the number of album sales over 1,000,000:

    const results = musicData
                    .filter((album) => album.sales >= 1000000)
                    .map((album) => `${album.artist} is a successful artist.`);

    console.log(results);

This returns four artists.

**Note:** On some of the above example I have not entered a 'named' function, i.e. ((argument) => {return something}). This is because the filter() method is a built in method, and so the callback function is entirely required.

What does this mean? **Well, you can replace 'for' loops with map(), and 'if' statements with filter().**

## 2.7. The Virtual DOM

React maintains an internal representation of the rendered UI. This means it can check and see if a particular DOM node is necessary and, if not, it will not create it until it is necessary. When a componenet's state changes, React checks to see if this component's UI needs to be updated. If it does, it will update the UI. If not, it will not.

In other words, since the DOM is a tree, and making a change to an element can require the entire tree to be rebuild (which is slow), React does just that which is necessary to render exactly what you want with the minimum amount of loading time.

This [article](https://medium.com/@gethylgeorge/how-virtual-dom-and-diffing-works-in-react-6fc805f9f84e) is a good explanation of what React does vis-a-vis the DOM.

# 3. Rendering UI with React

## 3.1. Creating UI Elements

Rather than a string template, React uses JavaScript objects to create the UI. We use these objects to display the look of our page, and React will take care of generating the DOM nodes required.

We can create our own components, and simply pass them data. This data will be used to generate the UI.

    React.createElement( /* type */, /* props */, /* content */ );

The React.createElement() is a top-level function that takes three arguments:

    1. The type of element to create (i.e. tag name <div>, <img>, etc. OR a component that we have created)
    2. The props to pass to the element (i.e. className, src, etc. OR null)
    3. The content to pass to the element (e.g. a line of text 'Hello World', or a child element. This is very broad as to what you can enter: string, number, array, object, null, plain text, JavaScript code, another React element, etc.)

We then use reactDOM.render() to render the element to the DOM on the page. For example:

    reactDOM.render(
        myElement,
        document.getElementById('root')
    )

**NOTE:** The 'myElement' variable is the element we created and consists of a JavaScript object.

**NOTE 2** The 'root' is the ID of the element in the HTML file that we want to render the element to. So, this 'hook' would be the sole element in the HTML file that we want to render our component to.

    <div id="root"></div>

    // In the HTML file

Since we have passed this element to reactDOM.render(), React will now generate the DOM nodes required to display the element.

### 3.1.1. Props

In the second argument we pass to createElement(), we can pass in properties. If we wanted an element to have a class, for example, we can simple use:

    React.createElement(
        'div',
        { className: 'my-class' },
        'Hello World'
    );

**NOTE** You cannot simply type 'class', since this is not something that the DOM can use. You must use 'className'. In other words, when you are creating the elements, remember that you are creating DOM nodes, not html strings. This could initially be problematic for you, as 'for' is not accepted by React as it is a reserved JavaScript keyword. Instead, you would need htmlFor.

### 3.1.2. Nesting with the Third Element

We can nest html elements easily within our first element by nesting it within the createElement() function:

    React.createElement(
        'div',
        { className: 'my-class' },
        React.createElement(
            'h1',
            null,
            'Hello World'
        )
    );

Another example would be an ordered list element:

    React.createElement(
        'ol',
        className: 'my-names-class',
        React.createElement('li', null, 'John'),
        React.createElement('li', null, 'Jane'),
        React.createElement('li', null, 'Jack')
    );

However, when it comes to arrays you would more likely store your array in a variable and pass it to the createElement() function:

    const people = ['John', 'Jane', 'Jack'];

    React.createElement(
        'ol',
        className: 'my-people',
        people.map((person) => React.createElement('li', { key: person.name }, person.name))
    );

**NOTE** We added a 'key' argument, since React prefers it this way! This is a unique identifier for each element. If you do not add a key, React will not know which element to update when a state changes.

## 3.2. JSX

JSX is a syntax extension to JavaScript. It is a way to write HTML in JavaScript, which allows for more readable code. The major example is the ability to use <> angle brackets inside JS, for example <div>Hello World</div>.

We can also use JavaScript in conjunction with JSX. For example, we can use JavaScript to create a component:

    const MyPeople = <ol>
        {people.map((person) =>
            <li key={person.name}>
                {person.name}
            </li>
        )}
    </ol>

**NOTE** Even though we are using a nice, concise, JSX syntax beginning with ol and ending in /ol, we are still using JavaScript with the createElement() method. This is because the DOM will compile JSX into JavaScript.

**NOTE 2** You can create _one_ element, no more. Everything else can be nested within it, but you cannot have two 'head-level' elements. For example, this will not work as h1 and ul are both at the head level and therefore this code is attempting to create two elements:

    const message = (
    <h1>All About JSX:</h1>
    <ul>
        <li>JSX</li>
        <li>is</li>
        <li>awesome!</li>
    </ul>
    );

## 3.3. Components in JSX

This is a key feature in React. This is where we bundle together our other JSX elements and make them reusable. When using an arrow function there is no need to _explicitly_ return the element, but with a traditionally-written function we need to include return.

Why is the component feature useful? Well, by combining all the seperate elements we can render and treat them as if they are one single element. Here's an example:

    const ContactList = () => {
        const people = [{ name:'John' }, { name:'Jane' }, { name:'Jack' }];

        return (
            <ol>
                {people.map((person) =>
                    <li key={person.name}>
                        {person.name}
                    </li>
                )}
            </ol>
        )
    };

ReactDOM.render(<ContactList />, document.getElementById('root'));

### 3.3.1. Traditional v Arrow Function Syntax

    const arrowFunction () => {}

    function traditionalFunction () {}

### 3.3.2. The 'this' Keyword

The 'this' keyword is a special keyword that is used to refer to the current object. In the example, the 'this' keyword refers to the ContactList component:

    const ContactList = () => {
        const people = [{ name:'John' }, { name:'Jane' }, { name:'Jack' }];

        return (
            <ol>
                {people.map((person) =>
                    <li key={person.name}>
                        {this.props.name}
                    </li>
                )}
            </ol>
        )
    };

## 3.4. create-react-app

In order to run JSX we need to use a compiler that will break the code down into JS to be run in the browser. Webpack is the tool I most often use for compiling web projects, and is also the most common in React, but FaceBook have created the create-react-app in order to do the same job for simplicity. The create-react-app is powered by react-scripts, and includes Babel, Webpack, Webpack-dev-server, and other tools.

To set up a project, just type npm create-react-app <project-name> in the terminal.

To read details on how to get React v18 working, check out the [React v18 docs](https://reactjs.org/blog/2022/03/08/react-18-upgrade-guide.html).

## 3.5. Composition

# 4. State Management

## 4.1. Props

In JavaScript, we pass data with arguments in functions. With React, we can pass data with props. For example, if we have a function that contains an array of usernames, but we want to make a fetchUser function that can be passed the username as an argument and just fetch that user's data. Here is what you would do to pass an argument to a function:

    const fetchUser = (username) => {
        // fetch the user
    };

    fetchUser('john');

But we can also do a similar thing with React components. In short, when we add JSX, we can simply add a custom attribute to the component and give it a particular user to display. Take for example if we have a component called 'User':

    const User = ({ username }) => {
        return <p>Username: {username}</p>
    };

    <User username='John' />

So any attributes that are added to a component will be accessible as props. All props are stored on the props handle, so to access the prop 'username' from within the component we simply need:

    const User = ({ username }) => {
        return <p>Username: {this.props.username}</p>
    };

In the case of a list of contacts (without object destructuring) it may be something like:

    const ContactList = (contacts) => {
        return (
            <ul>
                {contacts.map((contact) =>
                    <li key={contact.name}>
                        {contact.name}
                    </li>
                )}
            </ul>
        )
    };

In short, where you think of _functions passing arguments_, with React you can think of **components passing props.**

**NOTE** Props are immutable, or 'read-only' data. To change it you would need to update a parent component.

## 4.2. State

Whereas props are immutable, a component's state is mutable data that ultimately affects what is rendered on the page. State can change over time, for example, when a user clicks a button.

To add state to our components, all we need to do is leverage the React useState() hook. Put simply, with React, you need only two concerns: what state is my component in, and how does the UI appear based on that state.

To add a state to a component, you first need to import:

    import { useState } from 'react';

Since React has such a powerful tool in state management, it doesn't make sense to hardcode things such as a contact list into your code. Rather, you want to be able to add state to your components and have it automatically update (such as adding a contact, or deleting, editing, etc.).

After importing useState, you will need to set two variables in order to utilise it.

    1. A variable to hold that piece of state (e.g. the contacts we are using in our contact list)
    2. A variable function that allows us to change that piece of state (so we can modify or update it accordingly)

The syntaxt will look a little like this:

    const [contacts, setContacts] = useState([]);

useState takes in a single argument, which is the initial state. This is the state that will be used if the component is first rendered. To return to the contact list example, this can be the hard-coded details we had earlier.

    const [contacts, setContacts] = useState([
        { name: 'John', email: '
        ...
    ]);

**NOTE** When defining a component's initial state, avoid using props. This is because props are immutable, and therefore cannot be changed (e.g. NOT THIS > const [user, setUser] = useState(props.user); as you will not be able to alter the user when the state changes).

## 4.3. How to Change State

First, we need to insert a method in our component that will be responsible for, say, deleting a contact from our array.

    const removeContact = (contact) => {
        setContacts(contacts.filter((c) => c.id !== contact.id));

**NOTE** In the above code 'c' is used to refer to contacts. Thus, the id of 'c' does not equal the contact id that was passed in. Remember, filter() returns a new array, which now _does not_ contain the contact that was passed in.

Calling the setContacts method will not delete. In fact, it basically re-renders the UI based on the state, i.e. a contact having been deleted and therefore no longer existing in the array - which is a 'new' array.

Next, we need to pass this new removeContact component into our component responsible for rendering the UI. For example:

    return (
        <div>
            <h1>Contacts</h1>
            <ContactForm onSubmit={addContact} />
            <ContactList contacts={contacts} onDeleteContact={removeContact} />
        </div>
    );

You also need to ensure that the child component's are set up correctly. For example, if you have a component which renders a list of contacts upon being called by your root component, you need to alter the props to include onDeleteContact:

    const ListContacts = ({ contacts, onDeleteContacts }) => {
        ...
    };

Finally, (in the case of a delete button), you need to pass the removeContact method into the button component and have it run onClick:

    <button className="remove-contact" onClick={() => removeContact(contact)}>Delete</button>

**NOTE** At this point, we haven't added any persistence to a database, and so even if we delete contacts successfully so far, a quick reload of the page will bring them back.

## 4.4. PropTypes

A package that allows us to define the data type we want to see in our component (method, object, array, etc.). This is useful for debugging purposes, as it will help us to know what data we are expecting to be passed in, and will warn us if it sees something different. It requires installation:

    npm install prop-types

You then also need to import prop-types into the required component file.

    import PropTypes from 'prop-types';

Now we can add a property to our component. Outside of your component, just before the export statement, add the prop-types:

    MyComponent.propTypes = {
        name: PropTypes.string.isRequired,
        age: PropTypes.number.isRequired,
        onDeleteContact: PropTypes.func.isRequired
    };

You could also use a more precise requirement, for example:

    name: PropTypes.arrayOf(PropTypes.string).isRequired

This will require the array to be a list of strings.

PropTypes are probably most useful in warning us in the console if we are missing a prop, in which case it will give us a warning that something is coming back undefined.

## 4.5. Controlled Components

One issue that could be confusing is the status of forms, since they typically live in the DOM, yet we want to control it's state with React. This is where controlled components come in. Controlled components render a form, but the form does _not_ live within the DOM, but instead the source of truth for the form is in the component.

There are some great advantages to using controlled components for forms:

    1. We can immediately validate the input
    2. They allow you to conditionally enable or disable form buttons
    3. They enforce input formats

These are all aspects of updating the UI - the meat of React. So, rather than using a pop-up alert to notify us of an error, we can use a controlled component to render a form with an error message.

Returning to the idea of a contacts app, if we had thousands of contacts, we could use a controlled component as a search form. Essentially, as you type into the search box, you are allowing React to update the stateof the component, and therefore the rendered UI.

In the component that we want to apply the search form to (e.g. the list of contacts), create a new base div, and within it place your contacts div. Then place the search form within the base div. **NOTE** Don't forget to import { useState } again:

    import { useState } from 'react';

As before, we will need to create a variable within the component to refer to the state:

    const [query, setQuery] = useState('');

Next, you will need to have the value of the input field be the query of the state. To do this, you will first need to create a function that will update the state:

     const updateQuery = (query) => {
        setQuery(query.trim());
    };

Then finally we can return to our form input div:

    <input
        type="text"
        className="search-box"
        placeholder="Search..."
        value={query}
        onChange={(evt) => updateQuery(evt.target.value)}
    />

With all this done, however, you will not actually notice any change in terms of the rendering of the UI (other than the appearance of the search form). This is because the query is not being updated in the state, and therefore the UI is not re-rendered.

One more variable will be required within your component to re-render the UI:

    const showContacts =
        (query) === ''
            ? contacts
            : contacts.filter((c) =>
            c.name.toLowerCase().includes(query.toLowerCase())
        );

What the above code does is take the query as input and, if it is equal to an empty string (i.e. nothing has been entered) we will render our original contacts list.

Then we use '?' to check if the query is _not_ equal to an empty string, in which case we apply ':' to our contacts list, filter it down by name (c.name) and make sure the query is included in a name, making sure to match them both in lowercase so as to avoid 'Richard' not equalling 'richard'.

In short, if the query is empty, show all contacts, otherwise filter the contacts array by the query.

To top it off, rather than mapping over the entire contacts list in our component, we will just map over the showContacts list.

A nice touch would be to add a counter to show how many contacts out of the total you are showing currently, and also allow the user to return to a state of 'view all'. To do this, we can sandwich some JavaScript between the search form div and the contacts div:

    {
        showContacts.length !== contacts.length && (
            <div className="counter">
                <span>
                    Showing {showContacts.length} of {contacts.length}
                </span>
                <button onClick={clearQuery}>
                    Show all
                </button>
            </div>
        ))
    }

Then ensure you have built a simple function towards the top of the component that will return the query to an empty string:

    const clearQuery = () => {
        setQuery('');
    };

# 5. React Workflow

This is a really important read for figuring out your React development strategy: [Thinking in React](https://reactjs.org/docs/thinking-in-react.html).

# 6. Hooks

## 6.1. What are Hooks?

With the release of React 16.8 there is a feature called 'hooks', in order to simplify the syntax for developers to use during development: "They let you use state and other features without writing a class" - React Team

Above, we have already been using the useState() hook to update the state of our component. But there are many more, such as useEffect() and useContext().

In short, hooks allow us to access state and other features (such as life-cycle methods) without encapsulating them in a class. They can go directly into a component.

## 6.2. Side Effects

Side effects are anything that occurs 'outside' the scope of the way a component normally runs. A good example is fetching data with an asynchronous API call.

Why can't we just use a fetch request normally in the component? The problem is that a return statement needs to be free from side-effects as it essentially 'cuts' or 'ends' the code. In fact, we mainly want the return to use props for rendering the UI. The workaround is to utilise the useEffect() hook:

    import { useEffect } from 'react';

useEffect is a special method that each component has that allows us to run custom behaviour during certain times of the components life.

## 6.3. Using a Database

While we can, to an extend, store data within our components in hard code, it is much more likely that any true project will rely on a database somewhere. Grabbing the data will therefore require an API call.

First, assuming you have set up an API server and perhaps saved it in your project directory named 'utils', you need to import the API into your component:

    import * as ContactsAPI from '../utils/ContactsAPI';

Next you can delete any hard coded data that you want to store on your database (let's say it is the contacts list). Then you can set your setState() to an empty array in the component:

    const [contacts, setContacts] = useState([]);

Since an API call is a side-effect, we need to ensure that the component has useEffect() hook imported:

    import { useState, useEffect } from 'react';

Next, following the useState hook, we can write useEffect and pass it a callback function with any dependencies in an array. You can use either JS promises, or if you prefer you can use async await, to fetch your data and place it in the empty array:

    useEffect(() => {
        const getContacts = async () => {
            const res = await ContactsAPI.getAll();
            setContacts(res);
        };
        getContacts();
    }, []);

Now our app is set up so that our contacts are not coming in from the app itself, but from an external server.

**NOTE** The first argument for our useEffect() hook is a callback function, and the second argument is an array of dependencies. Since we have entered an empty array as our dependencies, this means that the useEffect() hook will only run once, when the component is first rendered.

## 6.4. Removing Data from the Database

If we are only removing data from the UI, we have the problem that the data will reappear if the user refreshers the browser page. Instead, we want the ability to completely remove the data from the database. In fact, we want it to do _both_: remove from the UI and database.

If our 'backend' database is set up correctly it should have a remove/delete method that can be called. In our app, we can then add the following within our component alongside the code for removing a contact from the UI:

    ContactsAPI.remove(contact);

Now we have persistence in our change! And it occurs both on the frontend UI and in the backend database.

## 6.5. Side Effect Cleanup

Cleanups can prevent memory leaks in our app by cancelling an asynchronous API call if the component is unmounted (i.e. not set in the DOM). Usually this is not an entirely necessary step, React themselves note that 'network requests' fall under a category not requiring cleanup. However, it is _good practise_ to do so.

A truly simple way to do this is simply to provide a return call on your useEffects method:

    useEffect(() => {
        const getContacts = async () => {
            const res = await ContactsAPI.getAll();
            setContacts(res);
        };
        getContacts();
        return () => {
            // cleanup
        };
    }, []);

Removing an event listener is also a good way to perform cleanup:

    useEffect(() => {
        window.addEventListener('resize', handleResize);
        return () => {
            window.removeEventListener('resize', handleResize);
        };
    });

Another good idea is to create a variable that tracks whether or not a component is mounted and, if it is, runs the side effect/custom logic, and updates the UI. But if the component is not mounted, we can cancel the side effect by returning false:

    useEffect(() => {

        let mounted = true;

        if (user.exists) {
        if (mounted) {
            setCurrentUser(user);
        }

        // ...
        }

        return () => {
        mounted = false;
    };

}, []);

## 6.6. Additional Hooks

    useReducer()
    useCallback()
    useMemo()
    useRef()
    useImperativeHandle()
    useContext()
    useDebugValue()
    useLayoutEffect()

It is worth reviewing the [Hooks Reference](https://reactjs.org/docs/hooks-reference.html#usecontext) for additional hooks and their information.

# 7. Routing

## 7.1. Single Page Applications

Although it sounds like it must be an application with just one page, a SPA is actually a web application that only requires the browser to make one call to the server to render the page and send it back to the user on their CPU. So, rather than receiving a home.html page, then clicking an 'about' page button that requires the browser to fetch about.html from the server, simply arriving once at the page is enough for all the inner pages to run.

In short, the SPA downloads the entire site contents at once. This improves performance, since when the user navigates to a new page, it is only an asynchronous JS request for _just_ the newly required content.

Of course, we also want the URL to be updated when a user navigates (for one thing, it is better for sharing links or bookmarking). This is one reason for using an SPA with a router.

## 7.2. React Router

React Router will turn our app into a SPA. It 'is a collection of navigational components that compose declaratively with your application'. Basically it provides numerous specialized components that allow you to manage the navigation of your app (creation of links, managing URL changes, provides transitions, etc).

## 7.3. Dynamically Rendering Pages

Taking the contacts app example, we would like to also be able to add contacts to the app. Since this is an entirely new component, we need to create it in a separate file (within the components directory). Next, we will need to set up a simple component for the time-being:

    const CreateContact = () => {
        return (
            <div className="create-contact">Create Contact</div>
        );
    };

    export default CreateContact;

Then we will import it into our app component:

    import CreateContact from './components/CreateContact';

And render it within our return call simply as: <CreateContact />. However, it would be better to render it conditionally, so that it only appears when the user clicks the 'create contact' button, for example.

First, we can add the state that will render CreateContact:

    const [screen, setScreen] = useState('list');

And then in the rendering logic return statement we can add a JS conditional statement, such as:

    return (
        <div>
        {
            screen === "list" && (<ListContacts contacts={contacts} onDeleteContact={removeContact} onNavigate={() = > {
                setScreen('create');
            }} />)
        }
        {
            screen === "create" && <CreateContact />
        }
        </div>
    );
    };

**NOTE** The && operator looks a bit funky as we are mixing JS and JSX. However, it is a valid technique known as 'valid AND expression', whereby the first statement is evaluated and if true, the second expression if run. Of course, if the first expression is false then the second expression (i.e. the part after the &&) is skipped.

We will also need a button to be able to switch between these two states. We can do this in our ListContacts component by adding it to the return statement with an anchor tag:

    return (
        ...
        <a href='#create' onClick={ onNavigate } className='add-contact'>
            Add Contact
        </a>
        ...
    );

**NOTE** This is essentially a _very_ basic 'vanilla' mock-up of how React Router works, rendering two different screens/pages depending on the state.

## 7.4. Install React Router

After all of that manual coding, why use React Router? Well, for one thing, if we press the back button in the browser it does not return us to the previously screen, which is certainly expected behaviour for any user. React Router does this for us.

    npm install react-router-dom

in your src/index.js file you will also need to import the Browser Router component:

    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

## 7.5. Broswer Router

The main function of this router is simply to listen for changes in the URL and present the correct screen to the user. To use this router, you need to wrap your render method in your src/index.js file in a BrowserRouter component:

    ReactDOM.render(
    <BrowserRouter>
        <App />
    </BrowserRouter>,
    document.getElementById("root")
    );

## 7.6. Navigation with < Link >

The link component is critical to the functioning of our app with Browser Router. When a link is clicked by the user, the link updates the URL in the browser, and the Browser Router will then present the correct screen to the user.

First, in your component file, import link:

    import { Link } from 'react-router-dom';

Next you will want to replace your anchor tags with link and replace the href with a 'to' attribute, remove the onClick handler, and the correponsing onClick handler that lives in the props above (e.g. if you had onClick={ onNavigate } then you would need to remove the onNavigate from the props in the main component line):

    const ListContacts = ({ contacts, onDeleteContact, }) => {
        ...

    <Link to='/create' className='add-contact'>
        Add Contact
    </Link>
        ...

**NOTE** The 'Link' in the component is the imported 'Link' with a capital letter, so using a lowercase l will cause an error.

Of course, you can also pass an object to Link to= to pass additional props to the link:

    <Link to={{
        pathname: "/courses",
        search: "?sort=name",
        hash: "#the-hash",
        state: { fromDashboard: true },
    }}>
        Courses
    </Link>;

Now you can pass the pathname, a query string, a hash to link to a particular part of a page, and a state object to pass additional information to the next page.

The documentation for the Link component can be found here [React Router](https://reactrouter.com/docs/en/v6/api#link).

## 7.7. Navigation with < Route >

With the Link component we can alter the URL in the browser and allow it to persist (so clicking back will return us to the previous 'page). However, we want to use the Route component that essentially will check if the URL matches a certain pathname and, if so, will render our chosen component.

This means that we no longer have to rely on our use of the screen state to determine the rendering of the page.

Firstly, import into your component:

    import { Route, Routes } from 'react-router-dom';

We can now remove all of our 'screen' logic from our app component:

~~const [screen, setScreen] = useState("list");~~

...

~~< div>~~
~~{~~
~~screen === "list" && (~~
~~<ListContacts~~
~~contacts={contacts}~~
~~onDeleteContact={removeContact}~~
~~onNavigate={() => {~~
~~setScreen("create");~~
~~}} />)~~
~~}~~
~~{~~
~~screen === "create" &&~~
~~< CreateContact />~~
~~}~~
~~</ div>~~

In place of the deleted logic, we can now include our components, while wrapping them in 'Routes' (simply because in React we need to return only _one_ base level component):

    return (
        <Routes>
        <Route
            exact path="/"
            element={
            <ListContacts contacts={contacts} onDeleteContact={removeContact} />
            } />
        <Route path="/create" element={<CreateContact />} />
        </Routes>
    );
    };

This now allows us to render the correct component depending on the URL.

## 7.8. Building a Form

Now that we have the link set up nicely to the create contact page, we can write a form in the CreateContact component. Of course, you want to make it more robust and interesting, but in essence, you could use:

import { Link } from 'react-router-dom';

    const CreateContact = () => {
        return (
            <div>
                <Link className="close-create-contact" to="/">
                    Close
                </Link>
                <form className="create-contact-form">
                    <input type="text" placeholder="Name" />
                    <input type="text" placeholder="Email" />
                    <input type="text" placeholder="Phone" />
                    <button>Add Contact</button>
                </form>
            </div>
        );
    };

    export default CreateContact;

### 7.8.1. Form Serialization

After creating the above form, we now have something that renders when a user clicks on a button to create contact from the 'home' page. However, we want to make sure that the form is submitted correctly, and that the data is stored in the correct place. In other words, we need some persistence.

For this, we need the data to be read by the app as regular JS, and for that we can use a package called form-serialize.

    npm install form-serialize

Then we can import the serialize function to our form component:

    import serialize from 'form-serialize';

Now we need to adapt our form to listen for a submit event, and add a handleSubmit method:

    import serializeForm from 'form-serialize';

    const CreateContact = ( onCreateContact ) => {

    const handleSubmit = (event) => {
        event.preventDefault();
        const values = serializeForm(event.target, { hash: true });

        if (onCreateContact) {
            onCreateContact(values);
        }
    };

    ...

    return (
        ...
        <form onSubmit={handleSubmit} className="create-contact-form">

        ...
    )
    };

## 7.9. Update Server with New Contact

Up to now, our create contact component form captures all the submitted data from the user, then serializes it, and then we pass all the form data (i.e. the values) to the onCreateContact props.

Next we can return to our app component and under the function that removes a contact we can now add our create a contact function:

    const createContact = (contact) => {
        const create = async() => {
            const res = await ContactsAPI.create(contact);
            setContacts(contacts.concat(res));
    };

    create();

Now we need to be sure to invoke this new createContact method. First, make sure to import useNavigate, and invoke it by saving it to a variable:

    import { Route, Routes, useNavigate } from 'react-router-dom';

    const App = () => {
        let navigate = useNavigate();

        ...

    };

The argument that navigate takes is the path to navigate to. In this case, we can send the user back to the 'homepage' after they have added a new contact:

    navigate("/");

Finally, we need to update our return value to reflect the CreateContact function with the value passed being 'contact' which is the 'value' argument that we passed from the form data within that function:

      <Route path="/create" element={<CreateContact onCreateContact={
        (contact) => {
          createContact(contact);
        }
      }
      />}

# 8. Learn More about React Router

Here is a course to learn more about [React Router](https://ui.dev/react-router).
And of course the [documentation](https://reactrouter.com/docs/en/v6).
