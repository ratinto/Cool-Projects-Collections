# 100 High-Quality JavaScript Interview Questions with Answers

This repository contains 100 carefully curated JavaScript interview questions, categorized by topic for easy navigation, along with concise answers. These questions range from beginner to advanced levels, covering core concepts, modern ES6+ features, asynchronous programming, and more. Use them to prepare for interviews, self-assess, or as a reference.

Questions are designed to test understanding, problem-solving, and practical application. Answers are provided to clarify concepts and provide practical insights.

## Table of Contents
- [JavaScript Basics](#javascript-basics) (Questions 1-20)
- [Variables and Data Types](#variables-and-data-types) (Questions 21-30)
- [Functions](#functions) (Questions 31-45)
- [Objects and Arrays](#objects-and-arrays) (Questions 46-60)
- [ES6+ Features](#es6-features) (Questions 61-75)
- [Asynchronous JavaScript](#asynchronous-javascript) (Questions 76-85)
- [DOM Manipulation](#dom-manipulation) (Questions 86-90)
- [Closures and Scope](#closures-and-scope) (Questions 91-95)
- [Prototypes and Inheritance](#prototypes-and-inheritance) (Questions 96-100)

## JavaScript Basics
1. **What is JavaScript, and how does it differ from Java?**  
   **Answer**: JavaScript is a high-level, interpreted scripting language for web development, enabling dynamic and interactive content. Java is a compiled, object-oriented language for general-purpose applications. JavaScript runs in browsers or Node.js, while Java requires a JVM. They differ in syntax, use cases, and execution environments.

2. **Explain the role of JavaScript in the web development triad (HTML, CSS, JS).**  
   **Answer**: HTML defines structure, CSS handles styling, and JavaScript adds interactivity and dynamic behavior, such as event handling, DOM manipulation, and fetching data.

3. **What are the different ways to embed JavaScript in an HTML page?**  
   **Answer**: Inline (`<script>code</script>` in HTML), external (`<script src="file.js"></script>`), and inline event handlers (e.g., `onclick="function()"`). External scripts are preferred for maintainability.

4. **Describe the execution context in JavaScript.**  
   **Answer**: An execution context is an environment where JavaScript code runs, consisting of a variable object, scope chain, and `this` binding. It includes global, function, and eval contexts.

5. **What is the difference between `undefined` and `null`?**  
   **Answer**: `undefined` means a variable is declared but not assigned a value. `null` is an explicit assignment of no value. Both are falsy, but `null` is intentional.

6. **How does JavaScript handle type coercion?**  
   **Answer**: Type coercion converts values to compatible types during operations (e.g., `"5" + 3` becomes `"53"`). Implicit coercion occurs in comparisons or arithmetic, often using `ToPrimitive`.

7. **Explain strict equality (`===`) vs. loose equality (`==`).**  
   **Answer**: `===` checks value and type (e.g., `5 === "5"` is false). `==` coerces types before comparison (e.g., `5 == "5"` is true). Use `===` for predictable results.

8. **What is NaN, and how can you check if a value is NaN?**  
   **Answer**: `NaN` represents an invalid number. Use `isNaN(value)` or `Number.isNaN(value)` (stricter, avoids coercion) to check.

9. **Describe the difference between `let`, `const`, and `var` declarations.**  
   **Answer**: `var` is function-scoped, hoisted, and reassignable. `let` is block-scoped and reassignable. `const` is block-scoped, non-reassignable, but mutable for objects/arrays.

10. **What is hoisting in JavaScript?**  
    **Answer**: Hoisting moves variable and function declarations to the top of their scope during compilation. Only declarations are hoisted, not initializations (e.g., `var x` is hoisted, but `x = 5` is not).

11. **Explain the event loop in JavaScript.**  
    **Answer**: The event loop manages asynchronous operations by processing the call stack and pushing tasks from the callback/task queue (e.g., timers, promises) when the stack is empty.

12. **What are primitive data types in JavaScript?**  
    **Answer**: String, Number, BigInt, Boolean, Undefined, Null, Symbol.

13. **How does JavaScript handle memory management and garbage collection?**  
    **Answer**: JavaScript uses automatic memory management with a garbage collector (e.g., mark-and-sweep) to reclaim memory from objects no longer referenced.

14. **What is the difference between `==` and `===` with examples?**  
    **Answer**: `==` coerces types: `5 == "5"` is true. `===` checks type and value: `5 === "5"` is false. Use `===` to avoid unexpected coercion.

15. **Explain truthy and falsy values in JavaScript.**  
    **Answer**: Falsy values (`false`, `0`, `""`, `null`, `undefined`, `NaN`) evaluate to false in conditions. All other values (e.g., `"0"`, `[]`, `{}`) are truthy.

16. **What is the `this` keyword in JavaScript, and how does its value change?**  
    **Answer**: `this` refers to the context object. In global scope, it’s `window` (browser). In methods, it’s the object. In arrow functions, it inherits from the outer scope.

17. **Describe the call stack and how it relates to recursion.**  
    **Answer**: The call stack tracks function execution. Recursion adds frames until a base case is reached. Excessive recursion may cause a stack overflow.

18. **What is the purpose of the `typeof` operator?**  
    **Answer**: `typeof` returns the type of a value (e.g., `typeof 42` returns `"number"`). It’s useful for type checking but has quirks (e.g., `typeof null` returns `"object"`).

19. **Explain the difference between global and local scope.**  
    **Answer**: Global scope is accessible everywhere; variables declared outside functions are global. Local scope is function- or block-specific, limiting variable access.

20. **How do you handle errors in JavaScript using try-catch?**  
    **Answer**: Wrap code in `try { code } catch (error) { handle error }`. Optionally, use `finally` for cleanup. Example: `try { JSON.parse(invalid) } catch (e) { console.log(e) }`.

## Variables and Data Types
21. **What are the six primitive data types in JavaScript?**  
    **Answer**: String, Number, BigInt, Boolean, Undefined, Null. Symbol is the seventh (ES6).

22. **How do you declare a constant variable that cannot be reassigned?**  
    **Answer**: Use `const`: `const x = 5;`. Objects/arrays declared with `const` are mutable but cannot be reassigned.

23. **Explain block scoping with `let` and `const`.**  
    **Answer**: `let` and `const` are limited to their block (e.g., `{}` in loops or conditionals). Unlike `var`, they don’t leak outside.

24. **What happens when you redeclare a variable with `var` in the same scope?**  
    **Answer**: `var` allows redeclaration without error, overwriting the previous value. Example: `var x = 1; var x = 2;`.

25. **Describe how JavaScript handles string concatenation vs. addition.**  
    **Answer**: `+` concatenates if any operand is a string (e.g., `5 + "3"` is `"53"`). For numbers, it adds (e.g., `5 + 3` is `8`).

26. **What is a Symbol in JavaScript, and when would you use it?**  
    **Answer**: `Symbol` creates unique identifiers. Use for object property keys to avoid collisions or to implement iterators. Example: `const id = Symbol('id')`.

27. **Explain the difference between shallow and deep copying of objects.**  
    **Answer**: Shallow copy (`Object.assign` or spread) copies top-level properties; nested objects share references. Deep copy (e.g., `JSON.parse(JSON.stringify(obj))`) clones all levels.

28. **How do you check if a variable is an array?**  
    **Answer**: Use `Array.isArray(value)` (e.g., `Array.isArray([1, 2])` returns `true`). `typeof` returns `"object"` for arrays.

29. **What is the BigInt data type, and how do you create one?**  
    **Answer**: `BigInt` handles integers beyond `Number.MAX_SAFE_INTEGER`. Create with `BigInt(123)` or `123n`.

30. **Describe template literals and their advantages over string concatenation.**  
    **Answer**: Template literals use backticks (`` ` ``) and `${}` for expressions (e.g., `` `Hi, ${name}` ``). They’re cleaner, support multiline strings, and avoid manual escaping.

## Functions
31. **What is a function declaration vs. function expression?**  
    **Answer**: Declaration: `function name() {}` (hoisted). Expression: `const name = function() {}` (not hoisted). Arrow: `const name = () => {}`.

32. **Explain arrow functions and their impact on `this`.**  
    **Answer**: Arrow functions (`=>`) have shorter syntax and inherit `this` from the outer scope, unlike regular functions where `this` depends on the caller.

33. **What are default parameters in functions?**  
    **Answer**: Default parameters set fallback values: `function greet(name = 'Guest') { return name; }`. Called as `greet()` returns `'Guest'`.

34. **How do you pass arguments to functions using rest parameters?**  
    **Answer**: Use `...args`: `function sum(...numbers) { return numbers.reduce((a, b) => a + b); }`. Collects all arguments into an array.

35. **Describe higher-order functions with an example.**  
    **Answer**: Functions that take or return functions. Example: `const multiplyBy = (n) => (x) => x * n; const double = multiplyBy(2);`.

36. **What is function currying, and how can you implement it?**  
    **Answer**: Currying transforms a function with multiple arguments into nested single-argument functions. Example: `const add = (a) => (b) => a + b; add(2)(3)` returns `5`.

37. **Explain the difference between `arguments` object and rest parameters.**  
    **Answer**: `arguments` is an array-like object in non-arrow functions. Rest parameters (`...args`) are true arrays, explicit, and work in arrow functions.

38. **What are immediately invoked function expressions (IIFE)?**  
    **Answer**: Functions executed immediately: `(function() { console.log('Run'); })();`. Used for initialization or avoiding global scope pollution.

39. **How do you create a recursive function?**  
    **Answer**: A function that calls itself until a base case. Example: `function factorial(n) { return n === 0 ? 1 : n * factorial(n - 1); }`.

40. **Describe pure functions and their benefits.**  
    **Answer**: Pure functions return the same output for the same input and have no side effects. Benefits: predictability, testability, and reusability.

41. **What is the difference between `call`, `apply`, and `bind`?**  
    **Answer**: `call` invokes with `this` and arguments individually. `apply` uses an array of arguments. `bind` returns a new function with fixed `this`.

42. **Explain closures in the context of functions.**  
    **Answer**: Closures allow a function to access its outer scope’s variables even after the outer function finishes. Example: `function outer() { let x = 1; return () => x; }`.

43. **How do you handle optional parameters in functions?**  
    **Answer**: Use default parameters or check for `undefined`: `function greet(name = 'Guest') { return name; }`.

44. **What is a generator function, and how does `yield` work?**  
    **Answer**: Generator functions (`function*`) return iterators. `yield` pauses execution, returning a value. Example: `function* gen() { yield 1; yield 2; }`.

45. **Describe memoization in functions.**  
    **Answer**: Memoization caches function results for inputs to improve performance. Example: `const memo = () => { const cache = {}; return (n) => cache[n] || (cache[n] = heavyCalc(n)); };`.

## Objects and Arrays
46. **How do you create an object literal in JavaScript?**  
    **Answer**: `const obj = { key: 'value' };`. Keys are strings or symbols; values can be any type.

47. **Explain prototypal inheritance.**  
    **Answer**: Objects inherit properties from their prototype. Example: `const obj = Object.create(parent);` links `obj` to `parent`’s prototype.

48. **What is the difference between `Object.create()` and `new Object()`?**  
    **Answer**: `Object.create(proto)` creates an object with `proto` as its prototype. `new Object()` creates a plain object with `Object.prototype`.

49. **How do you iterate over an object's properties?**  
    **Answer**: Use `for...in`, `Object.keys()`, `Object.values()`, or `Object.entries()`. Example: `for (let key in obj) { console.log(key, obj[key]); }`.

50. **Describe array methods like `map`, `filter`, and `reduce`.**  
    **Answer**: `map` transforms elements (`[1, 2].map(x => x * 2)` → `[2, 4]`). `filter` selects elements (`[1, 2].filter(x => x > 1)` → `[2]`). `reduce` aggregates (`[1, 2].reduce((sum, x) => sum + x, 0)` → `3`).

51. **What is destructuring for objects?**  
    **Answer**: Extracts properties into variables: `const { name, age } = { name: 'Alice', age: 30 };`. Supports defaults and renaming.

52. **How do you merge two objects?**  
    **Answer**: Use `Object.assign({}, obj1, obj2)` or spread: `{ ...obj1, ...obj2 }`. Later properties overwrite earlier ones.

53. **Explain the `spread` operator for objects.**  
    **Answer**: `...` copies enumerable properties: `const newObj = { ...obj, newKey: 'value' };`. Shallow copy, merges objects.

54. **What is the difference between `push` and `concat` for arrays?**  
    **Answer**: `push` adds elements to an array in place (`arr.push(4)`). `concat` returns a new array combining arrays (`arr.concat([4])`).

55. **How do you find the index of an element in an array?**  
    **Answer**: Use `indexOf` (first occurrence) or `findIndex` (with condition). Example: `[1, 2].indexOf(2)` returns `1`.

56. **Describe `forEach` vs. `for...of` loops.**  
    **Answer**: `forEach` runs a callback per element, no return value. `for...of` iterates values, supports `break`/`continue`. Example: `for (let x of arr) { console.log(x); }`.

57. **What is array destructuring?**  
    **Answer**: Extracts array elements: `const [a, b] = [1, 2];`. Supports rest (`...rest`) and defaults.

58. **How do you sort an array of objects?**  
    **Answer**: Use `sort` with a comparator: `arr.sort((a, b) => a.key - b.key);` for ascending by `key`.

59. **Explain shallow copy methods for arrays (`slice`, `spread`).**  
    **Answer**: `slice()` (`arr.slice()`) and spread (`[...arr]`) copy top-level elements. Nested objects share references.

60. **What is the purpose of `Object.keys()`, `Object.values()`, and `Object.entries()`?**  
    **Answer**: `Object.keys(obj)` returns property names. `Object.values(obj)` returns values. `Object.entries(obj)` returns `[key, value]` pairs.

## ES6+ Features
61. **What are ES6 modules, and how do you import/export them?**  
    **Answer**: Modules encapsulate code. Export: `export const x = 1;`. Import: `import { x } from './file.js';`. Supports default and named exports.

62. **Explain the `class` syntax in ES6.**  
    **Answer**: Syntactic sugar for constructor functions: `class MyClass { constructor() {} method() {} }`. Supports inheritance via `extends`.

63. **What is the `super` keyword in classes?**  
    **Answer**: `super` calls the parent class constructor or methods: `class Child extends Parent { constructor() { super(); } }`.

64. **Describe async/await and how it differs from Promises.**  
    **Answer**: `async/await` is syntactic sugar for Promises, making async code look synchronous. Example: `async function fetchData() { const res = await fetch(url); }`.

65. **What are optional chaining (`?.`) and nullish coalescing (`??`)?**  
    **Answer**: `?.` accesses properties safely (`obj?.prop`). `??` returns right operand if left is `null`/`undefined` (`x ?? defaultValue`).

66. **Explain the `for...of` vs. `for...in` loops.**  
    **Answer**: `for...of` iterates values of iterables (arrays, strings). `for...in` iterates enumerable object keys. Use `for...of` for arrays.

67. **What is a Proxy object, and when would you use it?**  
    **Answer**: `Proxy` intercepts operations on an object: `new Proxy(target, { get() {}, set() {} })`. Use for validation, logging, or custom behavior.

68. **Describe the `Set` data structure.**  
    **Answer**: `Set` stores unique values: `const set = new Set([1, 1, 2]);` (size `2`). Methods: `add`, `has`, `delete`.

69. **What is a `Map` vs. a plain object?**  
    **Answer**: `Map` stores key-value pairs, allows any key type (e.g., objects). Plain objects use strings/symbols as keys, simpler but less flexible.

70. **Explain private fields in classes (`#` prefix).**  
    **Answer**: `#field` declares private class fields, accessible only within the class: `class MyClass { #x = 1; }`.

71. **What are top-level await in modules?**  
    **Answer**: Allows `await` at module top level: `const data = await fetch(url);`. Only in ES modules.

72. **Describe logical assignment operators (`||=`, `&&=`, `??=`).**  
    **Answer**: `||=` assigns if falsy. `&&=` assigns if truthy. `??=` assigns if `null`/`undefined`. Example: `x ||= 1`.

73. **What is the `WeakMap` and `WeakSet`?**  
    **Answer**: `WeakMap`/`WeakSet` store weak references, allowing garbage collection if keys/objects are unreferenced. Use for memory-sensitive caching.

74. **Explain numeric separators (e.g., `1_000_000`).**  
    **Answer**: `_` improves readability of large numbers: `1_000_000` equals `1000000`. Ignored during computation.

75. **What is the `BigInt` literal syntax?**  
    **Answer**: Append `n` to integers: `123n`. Used for large numbers beyond `Number.MAX_SAFE_INTEGER`.

## Asynchronous JavaScript
76. **What is a Promise, and how do you create one?**  
    **Answer**: A `Promise` represents a future value: `new Promise((resolve, reject) => { resolve('done'); })`. States: pending, fulfilled, rejected.

77. **Explain Promise chaining with `.then()` and `.catch()`.**  
    **Answer**: Chain `.then()` for sequential operations, `.catch()` for errors: `promise.then(res => res + 1).catch(err => console.log(err))`.

78. **What is the purpose of `Promise.all()` and `Promise.race()`?**  
    **Answer**: `Promise.all([p1, p2])` resolves when all promises resolve or rejects on first rejection. `Promise.race([p1, p2])` resolves/rejects with the first settled promise.

79. **Describe callbacks and callback hell.**  
    **Answer**: Callbacks are functions passed as arguments. Callback hell is nested callbacks, making code hard to read. Promises/async solve this.

80. **How does `async/await` handle errors?**  
    **Answer**: Use `try/catch`: `async function fn() { try { await risky(); } catch (e) { console.log(e); } }`.

81. **What is the event loop’s role in async code?**  
    **Answer**: The event loop processes async tasks (e.g., promises, timers) from the task queue when the call stack is empty, ensuring non-blocking execution.

82. **Explain `fetch` API for HTTP requests.**  
    **Answer**: `fetch(url)` returns a Promise for HTTP requests: `fetch(url).then(res => res.json())`. Supports async/await for cleaner syntax.

83. **What are generators for async flows?**  
    **Answer**: Generators with `yield` pause execution, usable with async iterators for custom async flows, though less common with `async/await`.

84. **Describe debouncing and throttling in async contexts.**  
    **Answer**: Debouncing delays execution until no calls occur for a period. Throttling limits calls to a fixed rate. Used for event handling (e.g., scroll).

85. **How do you handle async iterators?**  
    **Answer**: Use `for await...of` for async iterables: `for await (const val of asyncIterable) { console.log(val); }`.

## DOM Manipulation
86. **What is the DOM, and how do you select elements?**  
    **Answer**: The DOM is a tree representation of HTML. Select with `document.querySelector('.class')`, `getElementById('id')`, or `getElementsByClassName('class')`.

87. **Explain `querySelector` vs. `getElementById`.**  
    **Answer**: `querySelector` uses CSS selectors, returns first match. `getElementById` is faster, matches ID only. Example: `document.querySelector('#id')`.

88. **How do you create and append elements dynamically?**  
    **Answer**: `const div = document.createElement('div'); div.textContent = 'Hi'; document.body.appendChild(div);`.

89. **What is event delegation?**  
    **Answer**: Attach an event listener to a parent to handle child events: `parent.addEventListener('click', e => { if (e.target.matches('.child')) { ... } });`.

90. **Describe the difference between `addEventListener` and inline events.**  
    **Answer**: `addEventListener` allows multiple listeners, dynamic binding: `el.addEventListener('click', fn)`. Inline (`onclick="fn()"`) is limited, less maintainable.

## Closures and Scope
91. **What is a closure, and provide a practical example?**  
    **Answer**: A closure is a function retaining access to its outer scope’s variables: `function outer() { let x = 1; return () => x++; } const fn = outer(); fn(); // 1`.

92. **Explain lexical scoping.**  
    **Answer**: Variables are resolved in the scope where a function is defined, not called. Closures rely on this.

93. **How do closures help in data privacy?**  
    **Answer**: Closures hide variables in a private scope: `function counter() { let count = 0; return { inc: () => count++ }; }`.

94. **What is the module pattern using closures?**  
    **Answer**: Wrap code in an IIFE, exposing only public methods: `(function() { let private = 1; return { get: () => private }; })()`.

95. **Describe scope chain resolution.**  
    **Answer**: JavaScript searches the scope chain (local → outer → global) for variables. Example: Inner functions access outer variables via closures.

## Prototypes and Inheritance
96. **What is the prototype chain?**  
    **Answer**: Objects inherit properties from their prototype, linked via `__proto__`. The chain ends at `Object.prototype`.

97. **How do you add methods to a prototype?**  
    **Answer**: `MyClass.prototype.method = function() {};` or use `class` syntax: `class MyClass { method() {} }`.

98. **Explain `Object.prototype.hasOwnProperty()`.**  
    **Answer**: Checks if a property exists directly on an object: `obj.hasOwnProperty('key')`. Excludes inherited properties.

99. **What is ES6 class inheritance with `extends`?**  
    **Answer**: `class Child extends Parent {}` inherits methods/properties. Use `super` to call parent constructor/methods.

100. **Describe `instanceof` operator and its relation to prototypes.**  
     **Answer**: `obj instanceof Constructor` checks if `Constructor.prototype` is in `obj`’s prototype chain. Example: `[] instanceof Array` is `true`.
