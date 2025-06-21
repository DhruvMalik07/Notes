# React JS Notes 2025

## Introduction

**REACT** → JavaScript Library

### Package Managers

- **npm**: Will download package in device and use it from there
- **npx**: Will not download package in device, rather it uses package for our project and then returns it back (kind of loan)

## JSX

**JSX** → Syntax extension, which enables us to write HTML in .js file (React feature)

## ES6 Modules

In JavaScript ES6 modules, there are two main types of exports: **default exports** and **named exports**.

The way you import a module depends on how it was exported.

**Explanation:**
- **Default Export**: This is the main export of a module, and it doesn't require curly braces when importing.
- **Named Export**: This is any additional export from the module, and it must be imported using curly braces.

**Note**: If we import named export without curly braces, then default export will be imported.

## JSX Wrapping

**Question**: Why do multiple JSX tags need to be wrapped?

**Answer**: JSX looks like HTML, but under the hood it is transformed into plain JavaScript objects. You can't return two objects from a function without wrapping them into an array. This explains why you also can't return two JSX tags without wrapping them into another single tag or a Fragment.

## Props

Props are the information that you pass to a JSX tag.

## Closures in React

JavaScript supports closures which means an inner function (e.g. `handleClick`) has access to variables and functions defined in an outer function (e.g. `Board`). The `handleClick` function can read the `squares` state and call the `setSquares` method because they are both defined inside of the `Board` function.

**In Hindi**: Agar ek function ke ander dusra function hai toh andar wala function bahar wale ki states padh sakta hai.

## Event Handling

| Code | Behavior |
|------|----------|
| `onClick={handleClick(0)}` | Calls the function immediately on render |
| `onClick={() => handleClick(0)}` | Calls the function when clicked |

## State Management

React state must not be mutated directly. So `.slice()` is used to create a copy of the array before modifying it.

**Important for**: Undo, Redo commands

## React.StrictMode

React.StrictMode is used during development to help find bugs and improve the quality of your code.

**It does things like:**
- Warn about unsafe lifecycle methods.
- Check for unexpected side effects.
- Detect legacy string ref usage.
- Double-invokes some functions in dev mode (like `useEffect`) to help catch bugs early.

**Note**: StrictMode has no effect in the production build — it's only for development debugging.

## JSX Basics

**JSX** = JS + HTML

React components need to return a single JSX element. So use **Fragments** (`<>` and `</>`) to wrap code.

## Data Binding

ReactJS uses **one-way data-binding**. This means child components are not able to update the data that is coming from the parent component. It is easy to debug and less prone to errors.

## Pure Components

**Pure component**: Only re-renders if the props or state it receives changes.

## Component Lifecycle

**Mounting**: The component is mounted on the DOM and rendered for the first time on the webpage.

## Refs

ReactJS **Refs** are used to access and modify the DOM elements in the React Application. They are used in cases where we want to change the value of a child component, without making use of props and state.

## Hooks

**Hooks** → Function that allows functional components in React to manage state, handle effects and some other React features without needing class components.

### useEffect

```javascript
useEffect(function, dependency)
```

'function' will run when there is change in value of 'dependency' array.

## Prop Drilling

**Prop drilling** means passing data (props) from a top-level component through many layers of components—even if some of those middle components don't need it, just to reach a deeply nested component.

**Solution**: React Context API, Redux

## State Management Tools

### React Redux

**React Redux** - State management tool (centralized control and easier debugging). Makes it easier to pass these states from one component to another irrespective of their position in the component tree and hence prevents the complexity of the application.

### Axios

**Axios** - Popular library, used to send asynchronous HTTP requests to REST endpoints. This library is very useful to perform CRUD operations.

## Reconciliation

**Reconciliation** is the process React uses to figure out how to efficiently update the DOM (Document Object Model) when changes occur in the UI. React's goal is to update the page as efficiently as possible, without unnecessary re-rendering or slow performance.

### How Reconciliation Works:

1. You change state or props.
2. React creates a new virtual DOM tree from your updated component.
3. React compares this new virtual DOM with the previous one (diffing).
4. React then updates only the changed parts in the real DOM.

## Performance Optimization

Optimizing React performance can be achieved using:

- **React.memo()** for preventing unnecessary re-renders.
- **Lazy loading** components with `React.lazy()` and `Suspense`.
- Using **useMemo()** and **useCallback()** hooks to memoize values and functions.
- Avoiding unnecessary state updates.

## Server-Side Rendering (SSR)

**Server-side rendering (SSR)** is the process of rendering a React application on the server and sending the fully rendered HTML to the client. This improves the initial page load performance and SEO.

## Client-Side Rendering (CSR) vs Server-Side Rendering (SSR)

In **CSR (Client-Side Rendering)**, the browser loads a basic HTML, then JavaScript takes over to render the content on the page.

**How it works:**
1. You load the website → browser gets a blank HTML with a `<div id="root"></div>`
2. React fetches data and renders everything in the browser

| Feature | CSR (Client-Side) | SSR (Server-Side) |
|---------|-------------------|-------------------|
| Initial load speed | Slower (blank page + JS) | Faster (HTML has content) |
| SEO friendliness | Poor (content loads later) | Great (content is preloaded) |
| Performance | Fast after first load | Can be slower on every request |
| Complexity | Easier to set up (Create React App) | Needs server (Next.js, Nuxt) |
| Best for | Apps (dashboards, SPA) | Blogs, news, SEO-heavy sites |

### When to Use Each

| Use CSR if... | Use SSR if... |
|---------------|---------------|
| SEO doesn't matter much | You care about SEO |
| Your app is interactive-heavy (e.g. Gmail) | Content must be visible immediately |
| You want a pure frontend app | You want better performance on first load |

## SEO and React

**SEO** is the practice of optimizing your website so that it appears higher in search engine results (like Google). For this, Google's bots (called crawlers) need to read your website's HTML content.

### SEO in CSR vs SSR

**In CSR:**
- The real content is rendered later using JavaScript (by React, Vue, etc.)
- Crawlers might not wait for the JavaScript to load or might not run it at all
- So, search engines may miss your content, which leads to poor SEO

**In SSR:**
- The server sends fully built HTML to the browser right away.
- Crawlers immediately see all the content
- ➡️ This makes your site SEO-friendly and easier to index

## Lazy Loading

**Lazy loading** is a performance optimization technique where content, code, or components are loaded only when needed, instead of loading everything at once when the app starts. It reduces initial load time.

## useRef Hook

**useRef**: React Hook that returns a mutable reference object (ref) that persists across renders.

**Key characteristics:**
- Unlike state variables, updating a ref does not trigger a component re-render.
- Access DOM elements directly
- Store values between renders without causing re-render

## WebSockets

**WebSockets** in Express.js and Node.js enable real-time, two-way communication between a website and its server. This allows for features like live chat, instant updates, and interactive experiences.

## Authentication Methods

### Google Auth vs JWT Auth

| Feature | Google Auth | JWT Auth |
|---------|-------------|----------|
| Who verifies user? | Google (external) | Your backend |
| Token type | ID token (JWT from Google) | Access token (JWT from your server) |
| Backend involvement | Minimal (verifying token) | Full (login, validation, token signing) |
| Implementation ease | Easier with Firebase/Auth libraries | Requires building login & token logic |
| Security | Very secure (backed by Google) | Secure, but up to your implementation |
| Use case | Social logins | Email/password systems, APIs |

### When to Use Each

| Use Google Auth if... | Use JWT Auth if... |
|----------------------|-------------------|
| You want fast, secure login | You need full control over login system |
| You want users to log in with Gmail | You're managing your own auth (e.g. users DB) |
| You're using Firebase | You're using a Node/Express backend | 