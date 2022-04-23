# REACT

React is a frontend library for building user interfaces. It is used for building web applications. If you just need a standard, static website, you can stick with HTML, CSS, and JavaScript. If you need dynamic pages, you can use React.

## MERN Stack

- **MongoDB**, which is the application’s database
- **Express**, which handles the application’s backend
- **React**, which is used to build the front end
- **Node**, which is the runtime environment for the application

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

Another key factor in React. Much of JavaScript is imperative code. To use a metaphor: if you are driving your car and want to keep the temperature at 70 degrees, you have to manage windows, the aircon, and air flow. You can achieve 70 degrees throughout your drive, but you need to keep adjusting the three different imperatives. With React, you use **declarative** code to say 'I want the temperature to remain at 70 degrees', and it handles all of the other determinants for you.
