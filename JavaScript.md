# JavaScript Notes

## Null vs Undefined

- **null**: Used to represent intentional absence of any object value.
  - `typeof null = object`

- **undefined**: Means a variable has been declared but has not been assigned a value (unintentional).
  - `typeof undefined = undefined`

## Language Characteristics

JavaScript is an **interpreted, dynamically typed language**. That means:
- It doesn't have a compile step like C++ or Java.
- Most errors are caught at runtime, during execution.

## Hoisting

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope (the global scope or function scope) during the compilation phase, before code execution.

- `var` is hoisted and initialized with `undefined`.
- `let` and `const` are hoisted but not initialized.
- **Arrow functions** (defined with `let` or `const`) are not hoisted and will throw a `ReferenceError` if called before being declared.

**Why Hoisting in JS**: JS processes declarations before execution.

**Major Benefit**: We can call functions early, even before its definition.

### Temporal Dead Zone

The Temporal Dead Zone is the time between:
- When a variable is hoisted, and
- When it is actually declared in the code.

During this time, accessing the variable will throw a ReferenceError.

## Closures

A closure is when a function remembers and accesses variables from its outer scope, even after that outer function has finished executing.

**Example:**
```javascript
function foo() { 
    let b = 1; 
    function inner() { 
       return b; 
    } 
    return inner; 
}
```

## Compiled vs Interpreted Languages

| Type | Description | Examples |
|------|-------------|----------|
| **Compiled language** | Translates entire code to machine code before running | C++, Java |
| **Interpreted language** | Translates and runs code line-by-line at runtime | JavaScript, Python |

## Event Bubbling

Event goes from child to parent.

## Equality Operators

| Operator | Name | Checks | Type Conversion? | Example |
|----------|------|--------|------------------|---------|
| `==` | Loose equality | Value only | ✅ Yes | `5 == '5'` → `true` |
| `===` | Strict equality | Value + Type | ❌ No | `5 === '5'` → `false` |

## Copying Objects

| Type | What It Does |
|------|-------------|
| **Shallow Copy** | Copies top-level values, but nested objects/arrays still refer to the same memory |
| **Deep Copy** | Copies everything, including nested objects, creating completely new memory |

### Shallow Copy Example

```javascript
const original = {
  name: "John",
  address: { city: "Delhi" }
};

const shallow = { ...original }; // OR Object.assign({}, original)

shallow.address.city = "Mumbai";

console.log(original.address.city); // ❗ "Mumbai" — changed in both!
// if changes are made in name in shallow, it won't affect name in original
```

### Deep Copy Example

```javascript
const original = {
  name: "John",
  address: { city: "Delhi" }
};

const deep = JSON.parse(JSON.stringify(original));

deep.address.city = "Mumbai";

console.log(original.address.city); // ✅ "Delhi" — original stays unchanged
```

## JavaScript Runtime

JavaScript is **single-threaded**, meaning it can only do one thing at a time. Yet it can handle things asynchronously using event loop and call stack.

### Call Stack - Execution Manager
- When a function is called → it goes on top of the stack.
- When it finishes → it is popped off the stack.
- The call stack handles synchronous code — one at a time.

### Event Loop - Middleman
- Constantly checks: "Is the call stack empty? If yes, let's run queued tasks."
- When asynchronous code (e.g., setTimeout, promises) is encountered, it's offloaded to the callback queue once its execution context is ready.
- The event loop continuously checks if the call stack is empty and moves tasks from the callback queue to the stack when it's empty, allowing asynchronous code to run without blocking the main thread.

## Performance Optimization

### Debouncing and Throttling

Debouncing and throttling are techniques used to optimize performance.

**Throttling**: A technique used to limit the number of times a function can be executed in a given time frame. It's extremely useful when dealing with performance-heavy operations, such as resizing the window or scrolling events, where repeated triggers can lead to performance issues.

**Debouncing**: Ensures that a function is only executed after a certain amount of idle time. Debouncing in JavaScript can be defined as the technique that is used to limit the number of times a function gets executed. Debouncing is useful when the event is frequently being triggered in a short interval of time like typing, scrolling, and resizing.

**Examples:**
- **Debouncing**: Wait until things stop
  - Imagine you're typing into a search box on Amazon.
  - It only sends a search after you stop typing for 500ms.
  - This avoids making too many API calls on every keystroke.

- **Throttling**: Limits how often something happens
  - If you scroll like crazy, still scrolling function runs only every 500ms (example), no matter how much you scroll

## React Concepts

### Props vs State

| Aspect | Props | State |
|--------|-------|-------|
| Similar to | Function parameters | Variables |
| Mutability | Immutable - read only | Mutable - both read & write |

### Virtual DOM and Diffing

- **Diffing Algorithm** in React JS differentiates the updated and previous DOM of the application.
- **Virtual DOM** only differs in the ability to write the screen like the real DOM; in fact, a new virtual DOM is created after every re-render.

### JSX and Transpilation

- In general, browsers are not capable of reading JSX and only can read pure JavaScript.
- The web browsers read JSX with the help of a transpiler.
- Transpilers are used to convert JSX into JavaScript.
- The transpiler used is called **Babel**.

### Keys in React

- **Key**: Unique identifier in React
- Helps track which items in a list have changed, been updated, or removed.
- Particularly useful when dynamically creating components or when users modify the list.

**Behavior:**
- **Without key**: React re-renders whole list
- **With proper key**: Only updates what changed

## JavaScript vs TypeScript

| Feature | JavaScript | TypeScript |
|---------|------------|------------|
| Typing | Dynamic (types known at runtime) | Static (types checked at compile time) |
| Compilation | Interpreted by browsers | Compiled to JavaScript |
| Errors | Caught at runtime | Caught at compile time |
| Tooling/Intellisense | Limited | Powerful autocompletion and type hints |
| Learning Curve | Easier for beginners | Slightly more complex (you learn types) |
| Scalability | Harder in large codebases | Ideal for large-scale apps |

### When to Use Each

| Use JavaScript if... | Use TypeScript if... |
|----------------------|----------------------|
| It's a small project or quick prototype | You're working on a large codebase |
| You want to learn web dev quickly | You want better code safety and tooling |
| You're writing basic scripts or dynamic behavior | You're using frameworks like Angular, Next.js |
| You're just learning the basics | You're working in a team | 