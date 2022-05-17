# Starting a Web Development Project

## Planning Steps

1. Plan the Draft (is it worth using Gantt charts, or similar software?)
2. Visit websites and narrow down to 3 websites to work from
3. Write a list of pages required
4. Sketch each page
5. Draw boxes around each component on each page and name them
6. Determine what happens in each component? E.g. is data being set, modified, or deleted? Use _actions_ and **data** (e.g. _get_ the **tweet**)
7. Decide what data will live in the store: **Rule of thumb**: Is it used by multiple components or mutated in a complex way? If not, the data can stay in a component. If it is used by multiple components, it should be moved to the store.
8. Draw up a file tree of actions, reducers, middleware, and components
