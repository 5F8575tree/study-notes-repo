# Redux

## Table of Contents

## What is Redux?

Essentially, Redux aims to simplify the management of state in React apps by providing one central stroe (tree) for all states. This hopefully means you do not get lost figuring out where your state is being stored.

With Redux, you can interact with this single store to: - Get the current state - Listen for changes - Update the state. **Data will be stored outside of the app and will simply be referenced within the app - keeping things more simple and clean.**

## The State Tree

One of the best ways to improve the quality of an app you build is to improve the predictability of the state that is being managed. Most bugs are caused by state mismanagement: for example, a mobile app showing you a notification alert without a notification existing.

The sole single place where our data is stored with Redux is the state tree. This means you do not have problems with duplicate data, and also you have full control over state management through a single source object.

## The Store

Contains the state tree, as well as the actions that can be manipulated on data with reducers: getting state, updating state, and listening for changes.

You can build out the Store in an index.js file, create a factory function to store objects, keep track of state, and then you can build methods to call on the store.

## Build the Store

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

### Listen to Changes
