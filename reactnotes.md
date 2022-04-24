# REACT

React is a frontend library for building user interfaces. It is used for building web applications. If you just need a standard, static website, you can stick with HTML, CSS, and JavaScript. If you need dynamic pages, you can use React.

## MERN Stack

- **MongoDB**, which is the application’s database
- **Express**, which handles the application’s backend
- **React**, which is used to build the front end
- **Node**, which is the runtime environment for the application

## Table of Contents

- [REACT](#react)
  - [MERN Stack](#mern-stack)
  - [Table of Contents](#table-of-contents)
- [Why Use React?](#why-use-react)
  - [Composition](#composition)
  - [Declarative Code](#declarative-code)
  - [Unidirectional Data Flow](#unidirectional-data-flow)
  - [React is Just JavaScript](#react-is-just-javascript)
  - [ES6 Syntax](#es6-syntax)
  - [Functional Programming](#functional-programming)
    - [Array map() Method](#array-map-method)
    - [Array filter() Method](#array-filter-method)
    - [Using filter() with map()](#using-filter-with-map)
  - [The Virtual DOM](#the-virtual-dom)
- [Rendering UI with React](#rendering-ui-with-react)
  - [Creating UI Elements](#creating-ui-elements)
    - [Props](#props)
    - [Nesting with the Third Element](#nesting-with-the-third-element)
  - [JSX](#jsx)

# Why Use React?

## Composition

We are used to using functions, and then using a single function that is composed of the other functions to return a value. In react, it works in the same way, but instead of writing functions to return some values, we compose the functions to **return UI elements.**

Composition is a way of combining **simple functions** to create more complex ones in **combination**.

This is one factor that makes React so useful. The _key difference_ between simply combining differing functions and using composition is based on the DOT idea ('Do One Thing'). In other words, with JavaScript we can combine functions to grab a user ID, build a url, and update the UI. But this is actually a 'monster' function that does three things. With React, you use composition to, for example, creating the following:

    <page>
        <article>
        <sidebar>
    </page>

This ensures that the page component actually contains the article and sidebar components.

## Declarative Code

Another key factor in React. Much of JavaScript is imperative code. To use a metaphor: if you are driving your car and want to keep the temperature at 70 degrees, you have to manage windows, the aircon, and air flow. You can achieve 70 degrees throughout your drive, but you need to keep adjusting the three different imperatives - you are telling it exactly what to do at each step.

With React, you use **declarative** code to say 'I want the temperature to remain at 70 degrees', and it handles all of the other determinants for you.

A code example would be the use of event listeners in JavaScript, and the use of the `onClick` attribute in React. 'onClick' can be simply written and assigned a function (e.g. 'handleSubmit').

## Unidirectional Data Flow

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

## React is Just JavaScript

React uses JavaScript syntax where it is easier to do so. For example, to loop through an array, you can just use .map() method that is built in to JS.

    const items = [1, 2, 3, 4, 5];
    const mappedItems = items.map(item => item * 2);

    console.log(mappedItems);

    // [2, 4, 6, 8, 10]

## ES6 Syntax

ES6 syntax is the new standard for JavaScript. It is a superset of JavaScript, and is used in React. Thus, you can use aroow functions, let/const variables, spread syntaxt (...), using functions as variables(e.g. const myFunctionVar = myFunction() ), and other ES6 features.

## Functional Programming

One of the greatest benefits of React is the ability to use **functional programming**. Functional programming is a programming paradigm that treats functions as first-class objects. This means that functions can be passed around, and can be returned from other functions. They can be stored in variables, and can be passed as arguments to other functions. They can also allow array methods such as map, filter, and reduce to be used on functions.

### Array map() Method

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

### Array filter() Method

As with the map() method, this method takes an array, with the function passed as an argument, and returns a new array. The difference is that this method filters out items from the original array based on a condition.

    const shortNames = names.filter((name) => name.length < 6);

To use our musicData example:

    const results = musicData.filter(album => album.name.length >= 10 && album.name.length <= 25);

    console.log(results);

This will return 3 objects from the musicData array with an album name between 10 and 25 characters long.

### Using filter() with map()

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

## The Virtual DOM

React maintains an internal representation of the rendered UI. This means it can check and see if a particular DOM node is necessary and, if not, it will not create it until it is necessary. When a componenet's state changes, React checks to see if this component's UI needs to be updated. If it does, it will update the UI. If not, it will not.

In other words, since the DOM is a tree, and making a change to an element can require the entire tree to be rebuild (which is slow), React does just that which is necessary to render exactly what you want with the minimum amount of loading time.

This [article]<https://medium.com/@gethylgeorge/how-virtual-dom-and-diffing-works-in-react-6fc805f9f84e> is a good explanation of what React does vis-a-vis the DOM.

# Rendering UI with React

## Creating UI Elements

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

### Props

In the second argument we pass to createElement(), we can pass in properties. If we wanted an element to have a class, for example, we can simple use:

    React.createElement(
        'div',
        { className: 'my-class' },
        'Hello World'
    );

**NOTE** You cannot simply type 'class', since this is not something that the DOM can use. You must use 'className'. In other words, when you are creating the elements, remember that you are creating DOM nodes, not html strings. This could initially be problematic for you, as 'for' is not accepted by React as it is a reserved JavaScript keyword. Instead, you would need htmlFor.

### Nesting with the Third Element

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

## JSX

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

## Components in JSX

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

### Traditional v Arrow Function Syntax

    const arrowFunction () => {}

    function traditionalFunction () {}

### The 'this' Keyword

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

## create-react-app

In order to run JSX we need to use a compiler that will break the code down into JS to be run in the browser. Webpack is the tool I most often use for compiling web projects, and is also the most common in React, but FaceBook have created the create-react-app in order to do the same job for simplicity. The create-react-app is powered by react-scripts, and includes Babel, Webpack, Webpack-dev-server, and other tools.

To set up a project, just type npm create-react-app <project-name> in the terminal.

To read details on how to get React v18 working, check out the [React v18 docs](https://reactjs.org/blog/2022/03/08/react-18-upgrade-guide.html).

## Composition

# State Management
