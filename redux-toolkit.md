## Redux
[Reudx Essentials](https://redux.js.org/tutorials/essentials/part-1-overview-concepts)

[Redux Core Concepts Note](https://github.com/jo-muuuuuu/penny-wave-notes/blob/main/redux.md)

[Reudx Fundamentals](https://redux.js.org/tutorials/fundamentals/part-1-overview)

Note that this tutorial (Redux Fundamentals) intentionally shows older-style Redux logic patterns that require more code than the "modern Redux" patterns with Redux Toolkit we teach as the right approach for building apps with Redux today, in order to explain the principles and concepts behind Redux. It's not meant to be a production-ready project.

### What is Redux?
Redux is really:

- A single store containing "global" state
- Dispatching plain object actions to the store when something happens in the app
- Pure reducer functions looking at those actions and returning immutably updated state

### What Does the Redux Core Do?
The Redux core is a very small and deliberately unopinionated library. It provides a few small API primitives:

- `createStore` to actually create a Redux store
- `combineReducers` to combine multiple slice reducers into a single larger reducer
- `applyMiddleware` to combine multiple middleware into a store enhancer
- `compose` to combine multiple store enhancers into a single store enhancer

Other than that, all the other Redux-related logic in your app has to be written entirely by you.

<mark>The good news is that this means Redux can be used in many different ways. The bad news is that there are no helpers to make any of your code easier to write.</mark>
## Redux Toolkit (RTK)
### Purpose of RTK
The Redux Toolkit package is intended to be the standard way to write Redux logic. It was originally created to help address three common concerns about Redux:

- "Configuring a Redux store is too complicated"
- "I have to add a lot of packages to get Redux to do anything useful"
- "Redux requires too much boilerplate code"

Redux Toolkit also includes a powerful data fetching and caching capability that we've dubbed "RTK Query". It's included in the package as a separate set of entry points. It's optional, but can eliminate the need to hand-write data fetching logic yourself.

These tools should be beneficial to all Redux users. Whether you're a brand new Redux user setting up your first project, or an experienced user who wants to simplify an existing application, Redux Toolkit can help you make your Redux code better.


### What Does RTK Do?
While these were the patterns originally shown in the Redux docs, they unfortunately require a lot of very verbose and repetitive code. Most of this boilerplate isn't necessary to use Redux. On top of that, the boilerplate-y code lead to more opportunities to make mistakes.

<mark><b>We specifically created Redux Toolkit to eliminate the "boilerplate" from hand-written Redux logic, prevent common mistakes, and provide APIs that simplify standard Redux tasks.</b></mark>
### RTK starts with two key APIs 
that simplify the most common things you do in every Redux app:

- `configureStore` <mark>sets up a well-configured Redux store</mark> with a single function call, including combining reducers, adding the thunk middleware, and setting up the Redux DevTools integration. It also is easier to configure than `createStore`, because it takes named options parameters.
- `createSlice` <mark>lets you write reducers</mark> that use the Immer library to enable writing immutable updates using "mutating" JS syntax like `state.value = 123`, with no spreads needed. It also automatically generates action creator functions for each reducer, and generates action type strings internally based on your reducer's names. Finally, it works great with TypeScript.

### RTK includes other APIs for common Redux tasks
- `createAsyncThunk`: abstracts the standard "dispatch actions before/after an async request" pattern
- `createEntityAdapter`: prebuilt reducers and selectors for CRUD operations on normalized state
- `createSelector`: a re-export of the standard Reselect API for memoized selectors
- `createListenerMiddleware`: a side effects middleware for running logic in response to dispatched actions

### RTK Query
Finally, the RTK package also includes "RTK Query", <mark>a full data fetching and caching solution</mark> for Redux apps, as a separate optional `@reduxjs/toolkit/query` entry point. It lets you define endpoints (REST, GraphQL, or any async function), and generates a reducer and middleware that fully manage fetching data, updating loading state, and caching results. It also automatically generates React hooks that can be used in components to fetch data, like `const { data, isFetching} = useGetPokemonQuery('pikachu')`

## Installation
### Create a React Redux App
Vite with Redux+TS template: `npx degit reduxjs/redux-templates/packages/vite-template-redux my-app`

### An Existing App
`npm install @reduxjs/toolkit`

`npm install react-redux` (for React bindings)

## What's Included
RTK includes these APIs:

`configureStore()`: wraps `createStore` to provide simplified configuration options and good defaults. It can automatically combine your slice reducers, adds whatever Redux middleware you supply, includes `redux-thunk` by default, and enables use of the Redux DevTools Extension.

`createReducer()`: that lets you supply a lookup table of action types to case reducer functions, rather than writing switch statements. In addition, it automatically uses the `immer` library to let you write simpler immutable updates with normal mutative code, like `state.todos[3].completed = true`.

`createAction()`: generates an action creator function for the given action type string.

`createSlice()`: accepts an object of reducer functions, a slice name, and an initial state value, and automatically generates a slice reducer with corresponding action creators and action types.

`combineSlices()`: combines multiple slices into a single reducer, and allows "lazy loading" of slices after initialisation.

`createAsyncThunk`: accepts an action type string and a function that returns a promise, and generates a thunk that dispatches `pending/fulfilled/rejected` action types based on that promise

`createEntityAdapter`: generates a set of reusable reducers and selectors to manage normalized data in the store

The `createSelector` utility from the `Reselect` library, re-exported for ease of use.

## RTK Quick Start
[Quick Start](https://redux-toolkit.js.org/tutorials/quick-start)

[TS Quick Start](https://redux-toolkit.js.org/tutorials/typescript)

[RTK Query Quick Start](https://redux-toolkit.js.org/tutorials/rtk-query)
