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
- `let` and `const` are hoisted but not initialized (Temporal Dead Zone).
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

## Input/Output (IO) Questions and Examples

### Object.keys()
Object.keys() method in JavaScript is used to retrieve an array of the enumerable property names of an object.
```js
const user = {
  name: "Alice",
  age: 25,
  city: "Delhi"
};
console.log(Object.keys(user)); // ["name", "age", "city"]
```

### JSON.parse()
JSON.parse() method is used to convert a JSON string into a JavaScript object.

### Floating Point Precision
```js
let x = 0.1 + 0.2;
let y = 0.3;
console.log(x == y); //false
```
JavaScript uses the IEEE 754 standard for representing numbers, which can't precisely represent some decimal values like 0.1. As a result, calculations like 0.1 + 0.2 yield slightly inaccurate results (0.30000000000000004 instead of 0.3). Therefore, comparisons like x == y may return false due to these small rounding errors.

### Type Coercion
When you use the == operator to compare values of different types, the operands will be converted to a common type before the comparison is made. This process is called type coercion.
```js
let x = false;
let y = "0";
let z = 0;
console.log(x == y); //true
console.log(x == z); //true
```

### Truthy/Falsy Values
```js
let x = [];
console.log(Boolean(x)); // true
```
In JS, an empty array [] is a truthy value when coerced to a Boolean.

### String and Number Operations
```js
let x = "5";
let y = 2;
console.log(x + y); //52 string
console.log(x - y); //3  number
```
+ => string concatenation
- => string to number

### this in Arrow Function
```js
let a = () => {
  console.log(this);
};
a();
```
Output: The code will output the global object (Window in a browser, or global in Node.js).

The behavior of this keyword inside a function depends on how the function is called. When a function is called with no explicit receiver (i.e., no object to the left of the . when calling the function), this will refer to the global object (Window in a browser, or global in Node.js).

In the given code, a is an arrow function that has no explicit receiver when it is called. Therefore, when a() is executed, this will refer to the global object, and the console.log statement inside the function will output the global object.

### Array + Array
```js
let x = [];
let y = [];
let z = x + y;
console.log(typeof z); //string
```
In JS, when you use the + operator with two arrays, or an array and any other object, both operands will be converted to strings before concatenation occurs.

### Logical NOT on String
```js
let x = "false";
let y = !x;
console.log(y); //false
```
In this code, x is a string containing the value "false". When you use the logical NOT operator (!) with a non-Boolean value, JavaScript will first convert the value to a Boolean and then negate it. Since "false" is a non-empty string, it is considered a truthy value when converted to Boolean, so !x will be the same as !true, which is false.

### Incrementing String
```js
let y = "1";
console.log(++y) //2
```
Since y is a string, it will be first converted to a number before it is incremented. The string "1" can be converted to the number 1, so ++y will also increment the value of y to 2.

### Arrays are Objects
```js
let x = [1, 2, 3];
console.log(typeof x);
```

### Spread Operator and Object Overwrite
```js
let x = { a: 1, b: 2 };
let y = { b: 3 };
let z = { ...x, ...y };
console.log(z);
```
In this code, two objects x and y are defined. x contains properties a and b, while y contains property b. Then, the spread operator ... is used to create a new object z that contains all of the properties from x and y.
When there are conflicting property names, as in this case with the property b, the value from the later object (in this case, y) will overwrite the value from the earlier object (x).
Therefore, when z is logged to the console, it will output { a: 1, b: 3 }.

### .map() Working in JS
```js
let x = [1, 2, 3];
let y = x.map((num) => {
  x.push(num + 3);
  return num + 1;
});
console.log(y);
```
In the code, an array x = [1, 2, 3] is mapped with a callback that returns num + 1 and also pushes num + 3 into x. Despite x being modified during the mapping, .map() only iterates over the array's initial length — 3 elements. This is because .map() determines its iteration count before execution begins.

As a result:
y becomes [2, 3, 4] — each original element incremented by 1.
x becomes [1, 2, 3, 4, 5, 6] — new elements added during iteration.
.map() ignores elements added after the loop starts.

### Array Holes
```js
let arr = [1, 2, 3];
arr[10] = 4;
console.log(arr.length);
// 11
```

### forEach()
forEach(): It does not return a new array and does not modify the original array. It's commonly used for iteration and performing actions on each array element.
```js
const arr = [1, 2, 3];
arr.forEach((num) => num * 2);
``` 