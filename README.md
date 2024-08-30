# Learn MERN Stack

- MERN stands for MongoDB, Express, React, and Node
- React will serve as the client side of the application, and provides all the visual aspects of the application
- Node and Express will power the server side of the application, such as changing the database
- We will be making APIs with Node and Express, which is how React will communicate with each other
- MongoDB will serve as our database, and a cloud service called Atlas
  - It is a NoSQL database that doesn't have relations
- Analogous to a restaurant: customers (React), the servers (Express and Node), and the chef (database).

# Creating Shopify Page

- You want to create a client folder that represents the frontend part of the application
- **Normalized.css** can be helpful for saving time on setup
  - It is a small CSS file that provides cross-browser consistency in the default styling of HTML elements
  - Just replace whatever is in `index.css` with normalized css

## Creating landing page

- For a browser with multiple pages, you want to set up a pages directory that will contain multiple pages
- You can use an extension called `ES7 React/Redux... snippets` that will easily create styled components
- You can type `rfce` to create a React functional component
- Or `rafc` to create an arrow function
- You might want to use an arrow function over a regular functional component because it creates a new function each time the component renders.
- You can also use styled components to make it faster to write styled HTML elements
  - It also creates unique classNames so you don't need to worry about changing the names of the elements
  - You can even wrap React elements into the styled components
  - Syntax is `styled.name"styles"`, and the quotes should be `.
- Outside of the return, you can also call a `Wrapper` component and you can target the elements within that element as well
- You can make a responsive display with `@media` annotation
  - Ex: For displaying an image, use `min-width` attribute and set the display
- Wrapper is only used for styling
- Something that might happen is you have a lot of components that you need to export out of the components folder. Therefore, something that you can do is to add `index.js` into the components and have all the imports there, then what you can do is just to `import {Element} from "../components"` and that will bring everything in
- You can also do it for pages

## Setting Up React Router

- React Router is arguably the most used solution when it comes to single page applications
- Want to import four different components, the usual four
- Connect to browser's URL with BrowserRoute, and Routes instead of Switch
- You usually set them up in `App.js`
- Route refers to the page, and it has an element attribute where you can just put the element directly into it
- If it's an error page, you can use a wild character \* to capture all other URLs
- The `Link` component can be used instead of a button, and you just need to keep the `classNames` the same and everything should work normally

## Setting up the global context

- Seems like the global context is actually its separate directory and used to store various things
- In this project, the files are `action.js`, `reducer.js`, `appContext.js`.
- Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.
- `React.createContext(defaultValue)`
  - Creates a Context object. When React renders a component that subscribes to this Context object it will read the current context value from the closest matching Provider above it in the tree.
  - The defaultValue argument is only used when a component does not have a matching Provider above it in the tree. This default value can be helpful for testing components in isolation without wrapping them. Note: passing undefined as a Provider value does not cause consuming components to use defaultValue.
- `React.Provider`
  - Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.
  - The Provider component accepts a value prop to be passed to consuming components that are descendants of this Provider. One Provider can be connected to many consumers. Providers can be nested to override values deeper within the tree.
  - `Context.Consumer`
    - A React component that subscribes to context changes. Using this component lets you subscribe to a context within a function component.
    - Requires a function as a child. The function receives the current context value and returns a React node. The value argument passed to the function will be equal to the value prop of the closest Provider for this context above in the tree. If there is no Provider for this context above, the value argument will be equal to the defaultValue that was passed to createContext().
- Use the value of a context with `const state = useAppContext()`, which a custom hook we wrote
- `useReducer`
  - The useReducer() hook in React lets you separate the state management from the rendering logic of the component. `const [state, dispatch] = useReducer(reducer, initialState)` accepts 2 argument: the reducer function and the initial state.
    - An alternative to useState. Accepts a reducer of type (state, action) => newState, and returns the current state paired with a dispatch method. (If you’re familiar with Redux, you already know how this works.)
    - useReducer is usually preferable to useState when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one. useReducer also lets you optimize performance for components that trigger deep updates because you can pass dispatch down instead of callbacks.

## Setting up the server

- In order to setup the server, you need to run `npm init -y`, which creates a `package.json` file that we can edit
- Once we have that, we can start setting up the Express Server
- For a long time, node uses something called CommonJS, but now there's also support for ES6 modules
  - CommonJS:
    - `const express = require('express')`
    - `const app = express()`
  - ES6
    - `import express from 'express'`
    - `const app = exepress()`
- To specify that it is a module, we need to denote that it is a module with `mjs` extension names or `type: "module"`
- You also need Nodemon to run the server, and make sure that the port of the server is different than the port of the frontend
- The website also needs some middleware to indicate when something is not found and also when you get an error
- Major difference between `not-found` and `error` middlewares is that `not found` is looking for requests that don't match any route, while `error` is looking for an error
- You want to place the `error` middleware always at the end

## Setting up the environment

- We need the `dotenv` package
- What we want to do here is to then connect to the MongoDB Atlas account
- After setting up the server and the environment, the next step will be to setup the authorization controller and route structure
- Once the servers are setup and in place, the next step will be to start creating the models

## Creating the models

- Now, we can actually set up the model for the user, and this involves controlling how the user logs in, etc
- We then need to create a Mongoose schema in order to utilize the functionalities in it
- We also need to validate the email, and we can do that by adding two additional properties to the schema
  - Validate needs a validator message and a validator function
