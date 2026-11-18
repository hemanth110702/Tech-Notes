<div id="top"></div>

# 📒 JavaScript — Interview Quick Reference

Core JS internals for interview prep — Namaste JavaScript series.
📚 [Namaste JavaScript](https://namastedev.com/learn/namaste-javascript) · Special Thanks to [Akshay Saini](https://www.youtube.com/@akshaymarch7)

<details>
<summary>Table of contents</summary>

- [1. Core Nature](#1-core-nature)
- [2. Execution Context](#2-execution-context)
- [3. Hoisting](#3-hoisting)
- [4. The Call Stack](#4-the-call-stack)
- [5. `this` & the Global Object](#5-this--the-global-object)
- [6. `undefined` vs `not defined`](#6-undefined-vs-not-defined)
- [7. Scope & Lexical Environment](#7-scope--lexical-environment)
- [8. `let`, `const` & `var`](#8-let-const--var)
- [8a. Block Scope & Shadowing](#8a-block-scope--shadowing)
- [9. Closures](#9-closures)
- [9a. Uses of Closures](#9a-uses-of-closures)
- [9b. Closure Memory & V8 Internals](#9b-closure-memory--v8-internals)
- [10. setTimeout & Closures](#10-settimeout--closures)
- [11. Event Loop & Async Model](#11-event-loop--async-model)
- [12. First-Class Functions & Function Types](#12-first-class-functions--function-types)
- [13. Callback Functions & Event Listeners](#13-callback-functions--event-listeners)
- [14. JS Engine Architecture & Google V8](#14-js-engine-architecture--google-v8)
- [15. Trust Issues with setTimeout()](#15-trust-issues-with-settimeout)
- [16. Higher-Order Functions & Polyfills](#16-higher-order-functions--polyfills)
- [17. Functional Array Methods — map, filter & reduce](#17-functional-array-methods--map-filter--reduce)
- [18. Callback Pitfalls — Callback Hell & Inversion of Control](#18-callback-pitfalls--callback-hell--inversion-of-control)
- [19. Quick Summary Table](#19-quick-summary-table)

</details>

---

## 1. Core Nature

| Property | Detail |
|---|---|
| **Single-Threaded** | One task at a time |
| **Synchronous by default** | Line-by-line execution |
| **Async via Event Loop** | Offloads heavy tasks to Web APIs / libuv |

---

## 2. Execution Context

Every time JS runs code, it creates an **Execution Context** with two phases:

| Phase | Also Called | What Happens |
|---|---|---|
| **Phase 1 — Memory** | Variable Environment | Variables & functions allocated in memory |
| **Phase 2 — Code** | Thread of Execution | Code runs top to bottom |

```
┌──────────────────────────────────────────────────┐
│               EXECUTION CONTEXT                  │
├─────────────────────────┬────────────────────────┤
│  MEMORY (key : value)   │         CODE           │
├─────────────────────────┤────────────────────────┤
│  a        → undefined   │                        │
│  square   → fn def {...}│  ← runs line by line   │
└─────────────────────────┴────────────────────────┘
```

---

## 3. Hoisting

> **What it is:** Before a single line executes, the JS engine runs a **Memory Creation Phase** — it scans the entire file and allocates memory for all variable and function declarations. This is hoisting.

### How Each Declaration Behaves

| Declaration | Hoisted As | Access Before Declaration |
|---|---|---|
| `function fn() {}` | Full function body | ✅ Works — callable immediately |
| `var` | `undefined` | Returns `undefined` (no crash) |
| `let` / `const` | Uninitialized (TDZ) | ❌ `ReferenceError` |
| `var fn = function() {}` | `undefined` | ❌ `TypeError` (calling undefined) |
| `var fn = () => {}` | `undefined` | ❌ `TypeError` (calling undefined) |

> **TDZ (Temporal Dead Zone):** `let`/`const` are allocated in memory but stay uninitialized until the engine actually reaches that line. Any access in that window → `ReferenceError`.

### Code Proof

```js
console.log(a);    // undefined      — var hoisted, initialized to undefined
console.log(b);    // ReferenceError — let is in TDZ
console.log(c());  // "c works"      — function declaration fully hoisted
console.log(d());  // TypeError      — var d exists but holds undefined

var a = 10;
let b = 20;
function c() { return "c works"; }
var d = function() { return "d works"; };
```

### Why Hoisting Was Designed This Way

Two real problems it solves:

**1. Top-down readability** — Wire up UI logic at the top, define functions below. Without hoisting, the engine crashes on line 1 because `validateForm` hasn’t been parsed yet.

```js
submitButton.onclick = validateForm;  // ✅ Works — validateForm is hoisted

function validateForm() { /* heavy logic */ }
```

**2. Mutual recursion** — If `A` calls `B` and `B` calls `A`, a single-pass engine always crashes (one must be defined first). Hoisting loads both into memory before either runs.

```js
function isEven(n) { return n === 0 ? true  : isOdd(n - 1); }
function isOdd(n)  { return n === 0 ? false : isEven(n - 1); }
// ✅ Both work — both hoisted before execution started
```

### 🎯 Interview Answer (Mechanically Sound)

> *"Hoisting is driven by how the Execution Context is created. During the **Memory Creation Phase** — before any code runs — the engine scans for all variable and function declarations and allocates memory for them.*
>
> *How they behave differs:*
> - **Function Declarations** are fully hoisted — their entire definition is stored, so they can be called before they appear in the code.
> - **`var`** is hoisted and initialized to `undefined`.
> - **`let`/`const`** are hoisted but stay **uninitialized** in the **Temporal Dead Zone (TDZ)** — accessing them throws a `ReferenceError`.
>
> *Architecturally, hoisting was designed to support mutually recursive functions and to let developers put main logic at the top, helper functions at the bottom — without the engine breaking."*

---

## 4. The Call Stack

> **Call Stack = manages the order of execution contexts (LIFO).**

- **GEC (Global Execution Context)** always sits at the bottom.
- Each function call **pushes** a new context; on return, it is **popped**.

```
┌──────────────────┐
│  fn() context    │  ← pushed on call, popped on return
├──────────────────┤
│  Global EC (GEC) │  ← always at bottom
└──────────────────┘
```

**Aliases:** Execution Context Stack · Program Stack · Control Stack · Runtime Stack · Machine Stack

---

## 5. `this` & the Global Object

- Each environment creates a global object on startup:
  - **Browser** → `window`
  - **Node.js** → `global`
- At the global level: `this === window // true`

```js
var i = 10;

console.log(i);         // 10
console.log(this.i);    // 10
console.log(window.i);  // 10  ← all equivalent at global scope

function a() {
  var x = 10;           // x is local — NOT on window
}
console.log(x);         // ReferenceError: x is not defined
```

---

## 6. `undefined` vs `not defined`

| Term | Meaning | Throws |
|---|---|---|
| `undefined` | Declared but not yet assigned | No error |
| `not defined` | Never declared — not in scope | `ReferenceError` |

> `undefined` is a real JS value — it is what the engine assigns during the memory phase as a placeholder, protecting the variable from the garbage collector before execution reaches it.

---

## 7. Scope & Lexical Environment

### Key Distinction

| Term | What it is |
|---|---|
| **Scope** | The *concept* — where is this variable accessible from? (developer-facing) |
| **Lexical Environment** | The *mechanism* — the internal data structure JS uses to implement scope (engine-facing) |

> **Scope = the “what.” Lexical Environment = the “how.”**

### How a Lexical Environment Is Built

Every Execution Context creation also creates a **Lexical Environment** with two parts:

**1. Environment Record** — the actual variable bindings (local memory)

**2. Outer Reference** — pointer to the parent Lexical Environment

- **Global LE’s** outer reference → `null`
- Every nested function’s LE outer reference → its parent’s Lexical Environment

### The Scope Chain

Variable lookup = walking this chain of outer references (a linked list of Lexical Environments):

```
inner’s LE → outer’s LE → Global LE → null (ReferenceError)
```

```js
function outer() {
  let city = "Mumbai";
  function inner() {
    console.log(city); // ✅ not in inner’s LE → walks to outer’s LE → found
  }
  inner();
}
```

### 🎯 Interview Answer

> *"Scope is the concept — where a variable is accessible. Lexical Environment is the engine’s internal mechanism that implements it: each execution context gets a Lexical Environment (local bindings + outer reference). The Scope Chain is the engine traversing that chain of outer references until the variable is found or null is hit. ‘Lexical’ means the chain is determined by where you wrote the function in the source, not where it’s called from."*

---

## 8. `let`, `const` & `var`

### Core Differences

| | `var` | `let` | `const` |
|---|---|---|---|
| **Scope** | Function-scoped | Block-scoped `{}` | Block-scoped `{}` |
| **Hoisting** | `undefined` | TDZ (uninitialized) | TDZ (uninitialized) |
| **Re-declaration** | ✅ Allowed | ❌ SyntaxError | ❌ SyntaxError |
| **Re-assignment** | ✅ Allowed | ✅ Allowed | ❌ TypeError |
| **Must initialize** | ❌ No | ❌ No | ✅ Yes |
| **Attaches to `window`** | ✅ Yes | ❌ No | ❌ No |

### Temporal Dead Zone (TDZ)

`let` and `const` are hoisted but left **uninitialized**. The TDZ is the gap between the start of the block and the line where they are actually declared. Accessing them in this window throws a `ReferenceError`.

```js
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 1;
```

> The engine **knows** `a` exists (it was hoisted) but refuses access — that's what makes it a `ReferenceError` and not a `not defined` error.

### Error Reference

**SyntaxError** — caught at parse time, code never runs:
```js
let a = 1;
let a = 1;   // SyntaxError: Identifier 'a' has already been declared

const b;     // SyntaxError: Missing initializer in const declaration
```

**ReferenceError** — accessing `let`/`const` before declaration, or accessing undeclared variable:
```js
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 1;

console.log(x); // ReferenceError: x is not defined
```

**TypeError** — re-assigning a `const`:
```js
const x = 1;
x = 11;      // TypeError: Assignment to constant variable
```

### `const` ≠ Immutable Value

`const` locks the **binding** (the variable reference), not the value itself. Objects and arrays declared with `const` can still be mutated:

```js
const obj = { name: "Alice" };
obj.name = "Bob";    // ✅ mutation is fine
obj = {};            // ❌ TypeError: re-assigning the binding
```

### 🎯 Interview Answer

> *"`var` is function-scoped and hoisted as `undefined`. `let` and `const` are block-scoped and hoisted but stay uninitialized in the TDZ — accessing them before their declaration throws a `ReferenceError`. `const` additionally requires initialization and locks the binding, not the value, so you can still mutate objects. `var` also attaches to the global `window` object; `let`/`const` don’t."*

---


## 8a. Block Scope & Shadowing

### What is a Block?

> A **block** is a pair of curly braces `{}`, also called a **compound statement**.

JS expects a single statement in places like `if`, `for`, `while`. A block lets you group multiple statements and pass them as one:

```js
if (true) doThis(); // single statement — fine

if (true) {         // block — groups multiple statements
  doThis();
  doThat();
}
```

### How Variables Are Hoisted Inside a Block

```js
{
  var a = 10;   // hoisted to global/function scope — lives OUTSIDE the block
  let b = 11;   // hoisted into Block scope — lives INSIDE the block only
  const c = 12; // hoisted into Block scope — lives INSIDE the block only
}

console.log(a); // ✅ 10 — var leaked out
console.log(b); // ❌ ReferenceError — let is block-scoped, gone after block ends
console.log(c); // ❌ ReferenceError — const is block-scoped, gone after block ends
```

### Shadowing

> **Shadowing** = declaring a variable inside a block with the same name as one in the outer scope. The inner declaration temporarily "shadows" the outer one — within that block, the inner binding takes over.

```js
var a = 5;    // Global scope
let b = 10;   // Script scope (global let)
const c = 15; // Script scope (global const)

{
  var a = 20;    // Same var 'a' — modifies the SAME global binding (no new 'a' created)
  let b = 25;    // New 'b' — block scope, shadows outer 'b'
  const c = 30;  // New 'c' — block scope, shadows outer 'c'

  console.log(a); // 20
  console.log(b); // 25
  console.log(c); // 30
}

console.log(a); // 20 — var was the same binding all along, mutation persists
console.log(b); // 10 — outer 'b' is back, block 'b' is gone
console.log(c); // 15 — outer 'c' is back, block 'c' is gone
```

> **Key insight:** `var a` inside a block does NOT create a new `a` — it points to the same global `a` because `var` ignores block boundaries. `let`/`const` create a fresh binding within the block.

> **Scope binding rule:**
> - `var` → binding lives in the **nearest enclosing function scope** (or global if no function wraps it)
> - `let`/`const` → binding lives in the **nearest enclosing block** `{}`
>
> This is why `var` inside any block — `if`, `for`, plain `{}` — leaks out, and `let`/`const` don’t.

### Illegal Shadowing — `var` Cannot Shadow `let`/`const`

```js
let a = 5;    // registered in Script scope
const b = 6;  // registered in Script scope

{
  var a = 10; // ❌ SyntaxError: Identifier 'a' has already been declared
  var b = 7;  // ❌ SyntaxError: Identifier 'b' has already been declared
}
```

**Why this throws:** `var` is function-scoped — it ignores the block and hoists to the same Script/global scope where `let a` already exists. The engine sees two declarations for `a` in the same scope during the Memory Creation Phase → collision → `SyntaxError` before any code runs.

> `let`/`const` CAN shadow `var` (block scope creates a genuinely new binding), but `var` CANNOT shadow `let`/`const` (because `var` hoisting collapses it into the same scope).

```js
var x = 5;
{
  let x = 10; // ✅ Legal — let creates a new block-scoped binding, doesn't collide
  console.log(x); // 10
}
console.log(x); // 5
```


### Block Scope vs Function Scope

This is the most interview-critical difference:

```js
// var leaks out of blocks
if (true) {
  var a = 10;
}
console.log(a); // 10 — leaked out

// let/const are contained
if (true) {
  let b = 10;
}
console.log(b); // ReferenceError: b is not defined
```

## 9. Closures

### What a Closure Is

> A **closure** is a function that **retains access to its outer (lexical) scope** even after that outer function has returned and its execution context has been popped off the call stack.

This works because JS keeps the outer function’s **lexical environment alive** in memory as long as the inner function holds a reference to it.

```js
function outer() {
  let count = 0;            // this variable stays alive

  return function inner() {
    count++;
    console.log(count);
  };
}

const increment = outer();  // outer() returns; its EC is popped
increment(); // 1            // but count is still accessible — that’s a closure
increment(); // 2
increment(); // 3
```

### 🎯 Interview Answer

> *"A closure is a function bundled together with its lexical environment — specifically, the outer variables it references. When the outer function returns, its execution context is popped off the stack, but JS keeps the lexical environment alive in memory because the inner function still holds a reference to it. This lets the inner function read and mutate those outer variables long after the outer function has finished. DevTools only shows `[[Closure]]` when there is at least one outer variable actually captured — if the inner function doesn’t reference anything from outside, there’s nothing to display."*

> ⚠️ **Snapshot vs. Reference:** Closures capture a **reference to the variable binding**, NOT a snapshot of its value at declaration time. If code modifies a variable after scheduling a callback, the callback reads the **updated value** when it runs — because the value is read at invocation time, not at creation time.

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 9a. Uses of Closures

- Module design pattern
- Currying
- Functions like `once` (run-only-once guards)
- Memoization
- Maintaining state in the async world
- `setTimeout` / `setInterval` callbacks
- Data privacy / encapsulation

### ⚠️ Disadvantages of Closures

- **Memory Consumption**: Closed-over variables are stored in heap memory and cannot be garbage-collected as long as the closure reference is reachable.
- **Risk of Memory Leaks**: Uncleaned closures (e.g. neglected event listeners, intervals, or large unused variables trapped in scope) consume memory indefinitely if not dereferenced.
- **Performance Overhead**: Resolving identifiers across nested outer scopes requires scope-chain traversal; excessive closures add heap allocation costs compared to standard functions.

```js
function x() {
  var a = 5;
  function y() {   // y forms a closure over 'a'
    console.log(a);
  }
  return y;
}

var z = x();
z(); // 5 — outer x() is gone, but 'a' is still alive via closure
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 9b. Closure Memory & V8 Internals

> **V8 creates one shared Closure Context object per outer function scope** — not one per inner function.

### How It Works (Step by Step)

1. A function is invoked → local memory space created.
2. If **any** inner function references an outer variable, V8 creates a single **hidden Closure Context object on the heap**.
3. V8 copies every variable referenced by **any** inner function into this one shared object.
4. All inner functions created in that scope are handed a **pointer to the same shared object**.

> You don't have multiple isolated closures — you have **one shared closure context per outer function**, and every inner function is tethered to it.

### Memory Management & Closure Leak

```js
function factory() {
  const massiveData = new Array(1000000).fill('data');
  const secretKey = 'alpha-1';

  const helper = function() {
    console.log(massiveData); // helper captures massiveData → goes into shared context
  };

  // Even though helper is not returned, massiveData stays alive
  // because it's in the shared closure context — execute holds that context.
  // Fix: nullify massiveData before returning execute.
  // massiveData = null; ← frees the heap reference

  return function execute() {
    console.log(`Executing with key: ${secretKey}`);
  };
}

const myFunc = factory();
// execute only needs secretKey, but massiveData is also kept alive
// in the shared closure context because helper captured it.
```

> ⚠️ **Closure leak gotcha:** If one inner function captures a large variable, that variable stays alive for the lifetime of **all** returned closures from that scope — even if the returning function never uses it. Null it out explicitly when done.

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 10. setTimeout & Closures

> `setTimeout` callbacks form a **closure** over the variables in their enclosing scope. Whether they capture the same binding or a fresh one depends on `var` vs `let`.

### Ex 1 — Basic closure capture with `var`

```js
function fun() {
  var i = 5;
  setTimeout(() => {
    console.log(i); // 5 — closure over 'i', logged after 1s
  }, 1000);
  console.log("JavaScript"); // runs immediately (sync)
}
fun();
// Output: "JavaScript" → 5
```

> The sync `console.log` runs first; the callback fires after 1 s and reads `i` from its closed-over scope.

### Ex 2 — `let` gives each iteration its own binding

```js
function fun() {
  for (let i = 1; i <= 5; i++) {
    setTimeout(() => {
      console.log(i); // 1, 2, 3, 4, 5 — each callback closes over its own 'i'
    }, i * 1000);
  }
}
fun();
// Output: 1 (after 1s), 2 (after 2s), 3 (after 3s), 4 (after 4s), 5 (after 5s)
```

> `let` is re-bound per iteration — each closure captures a distinct `i`.

### Ex 3 — Fixing `var` with a wrapper function (classic IIFE pattern)

```js
function fun() {
  for (var i = 1; i <= 5; i++) {
    function count(x) {
      setTimeout(() => {
        console.log(x); // 1, 2, 3, 4, 5
      }, x * 1000);
    }
    count(i); // each call to count() creates a new scope with its own 'x'
  }
}
fun();
// Output: 1 (after 1s), 2 (after 2s), 3 (after 3s), 4 (after 4s), 5 (after 5s)
```

> `var i` is shared across all iterations, so without the wrapper every callback would log `6`. Passing `i` into `count(x)` gives each callback its own frozen copy.

| Feature | `var` in loops | `let` in loops |
|:---|:---|:---|
| **Scope** | Function / Global scope | Block scope `{}` |
| **Binding count** | One shared instance for all iterations | Brand-new binding created per iteration |
| **Closure behavior** | Every callback sees the same variable — reads the **final loop value** | Each callback captures its own isolated iteration value |
| **Pre-ES6 fix** | Wrap in IIFE or helper function (`count(x)`) to create a fresh scope per pass | `let` handles it natively |

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 11. Event Loop & Async Model

### Execution Priority Chain

**Call Stack (Sync) → Microtask Queue (drain all) → Macrotask Queue (one at a time)**

1. **Synchronous code** — runs line-by-line on the Call Stack until empty.
2. **Microtasks** (`Promise.then`, `queueMicrotask`, `process.nextTick`) — highest async priority; the engine completely drains the queue before touching any macrotask or rendering.
3. **Macrotasks** (`setTimeout`, `setInterval`, `setImmediate`, I/O) — picked up one at a time, only when the Call Stack **and** Microtask Queue are both empty.

| Component | Role | Examples |
|---|---|---|
| **Call Stack** | Executes JS synchronously | All sync code |
| **Web APIs / libuv** | Handles async tasks off-thread | fetch, timers, I/O |
| **Microtask Queue** | High-priority; runs before macrotasks | `Promise.then`, `queueMicrotask` |
| **Macrotask Queue** | Lower-priority | `setTimeout`, `setInterval`, I/O callbacks |

```js
console.log("1");
setTimeout(() => console.log("2"), 0);        // Macrotask
Promise.resolve().then(() => console.log("3")); // Microtask
console.log("4");
// Output: 1 → 4 → 3 → 2
```

### 🎯 3-Step Mental Trace Model

When reading any async snippet:
1. **Trace sync first** — run all top-level statements, note variable mutations, push callbacks to Micro/Macro queues.
2. **Drain microtasks** — execute all Promise callbacks in FIFO order; closure variables read their **current** value at invocation time.
3. **Process macrotasks** — pop one at a time; if a macrotask queues a new microtask, that microtask runs before the next macrotask.

---

### 🌐 Web APIs — Browser Superpowers

The JavaScript engine itself has **no built-in timer, DOM access, network fetch, or local storage** — it only possesses the Call Stack and Memory Heap. The host browser environment provides these capabilities as **Web APIs** and exposes them on the global `window` object:

| Web API | Provided Capability | Exposed Through |
|---|---|---|
| `setTimeout()` / `setInterval()` | Timer & delay scheduling | `window.setTimeout` |
| DOM APIs (`document.*`) | HTML DOM tree inspection & mutation | `window.document` |
| `fetch()` | Network / HTTP requests | `window.fetch` |
| `localStorage` / `sessionStorage` | Persistent client-side key-value storage | `window.localStorage` |
| `console` | Debug stream / logging output | `window.console` *(even `console.log` is a Web API!)* |

---

### 🚨 Queue Starvation (Microtask Priority Trap)

The Event Loop prioritizes the **Microtask Queue** over the Callback (Macrotask) Queue. It completely drains the Microtask Queue before it picks up a single Macrotask.

> ⚠️ **Starvation Warning:** If a microtask continuously schedules another microtask (e.g. recursive `Promise.resolve().then(...)` loops), the Call Stack never yields to the Callback Queue. Timers (`setTimeout`), DOM event handlers (`click`, `scroll`), and UI rendering will **starve** and cause the page to freeze.

| Queue | Tasks Included | Processing Strategy |
|---|---|---|
| **Microtask Queue** | `Promise` callbacks (`.then`, `.catch`, `.finally`), `queueMicrotask()`, `MutationObserver` | **Drained completely** per Event Loop tick |
| **Callback (Macrotask) Queue** | `setTimeout()`, `setInterval()`, DOM event listeners | **One task picked** per tick after microtasks clear |

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 12. First-Class Functions & Function Types

> In JavaScript, functions are **first-class citizens** (first-class objects) — they can be treated like any other value (assigned to variables, passed as arguments, and returned from functions).

### Function Statement vs. Function Expression

The defining technical difference between a Function Statement (Declaration) and a Function Expression is **hoisting**.

```js
a(); // ✅ Works: "a called"
b(); // ❌ TypeError: b is not a function

// Function Statement (aka Function Declaration)
function a() {
  console.log("a called");
}

// Function Expression
var b = function () {
  console.log("b called");
};
```

| Type | Syntax | Hoisting Behavior | Early Invocation |
|---|---|---|---|
| **Function Statement** (Declaration) | `function a() {}` | Fully hoisted with body definition | ✅ Executes normally |
| **Function Expression** (`var`) | `var b = function() {}` | Variable hoisted as `undefined` | ❌ `TypeError: b is not a function` |
| **Function Expression** (`let`/`const`) | `const b = function() {}` | Hoisted in TDZ (uninitialized) | ❌ `ReferenceError: Cannot access 'b'` |

---

### Anonymous Functions

A function without an identifier (name).

```js
// Standalone anonymous function -> SyntaxError
// function () {} // SyntaxError: Function statements require a function name

// Used as a value (Expression)
var greet = function () {
  console.log("Hello");
};
```

> ⚠️ **Syntax Rule:** ECMAScript requires function statements to have a name. An anonymous function cannot stand alone as a statement; it must be used as an expression (assigned to a variable, passed as a callback, or wrapped in an IIFE).

---

### Named Function Expression

A function expression where the function has an internal identifier.

```js
var c = function fun() {
  console.log(fun); // ✅ Works — 'fun' exists inside its own local scope
  console.log("c called");
};

c();     // ✅ Works: "c called"
fun();   // ❌ ReferenceError: fun is not defined
```

> ⚠️ **Scope Trap:** The identifier `fun` is **not** created in the outer enclosing scope. It is bound strictly inside the function's own local environment record (useful for recursion and stack traces). Outside callers must invoke `c()`.

---

### Parameters vs. Arguments

| Concept | Definition | Example |
|---|---|---|
| **Parameters** | Identifiers declared in the function definition (placeholders) | `function abc(param1, param2) {}` |
| **Arguments** | Actual values/expressions passed to the function at invocation | `abc("val1", 42)` |

---

### First-Class Functions (First-Class Citizens)

The ability of functions to be treated as values:
1. **Assigned to a variable** or stored in data structures.
2. **Passed as arguments** to other functions (callbacks).
3. **Returned from other functions** (higher-order functions / closures).

```js
// 1. Pass function as an argument (Callback)
function greet(callback) {
  callback();
}

function sayHi() {
  console.log("Hi!");
}

greet(sayHi); // Passed as argument

// 2. Return a function from another function (Higher-Order Function)
function outer() {
  return function () {
    console.log("Returned inner function");
  };
}

const innerFn = outer();
innerFn();
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>


## 13. Callback Functions & Event Listeners

A **callback function** is a function passed as an argument to another function, which is then invoked inside that function to execute a routine or action.

```js
// Synchronous Callback Example
function x(y) {
  console.log("x");
  y(); // y is the callback function
}

x(function y() {
  console.log("y");
});
// Output: "x" → "y"
```

---

### ⚡ The Power of Callbacks (Async in Single-Threaded JS)

JavaScript is **synchronous and single-threaded** — it has only one Call Stack and can execute only one command at a time.

- Callbacks enable asynchronous behavior by delegating tasks to browser Web APIs (timers, network requests, DOM events).
- The main thread does not wait; the callback runs later via the Event Loop once the Call Stack is empty.

```js
// Asynchronous Callback Example
console.log("Start");

setTimeout(function () {
  console.log("Timer finished (5s)");
}, 5000);

console.log("End");
// Output: "Start" → "End" → (after 5s) "Timer finished (5s)"
```

---

### 🎧 Closures with Event Listeners

Event listeners commonly rely on closures to maintain private state across user interactions without polluting the global scope.

```html
<button id="my-btn">Click Me</button>
```

```js
function attachClickListener() {
  let count = 0; // Data-hiding via closure

  document.querySelector("#my-btn").addEventListener("click", function handleClick() {
    console.log("Button clicked:", ++count);
  });
}

attachClickListener();
```

#### Scope Inspection in DevTools
When inspecting the `#my-btn` listener in Chrome DevTools (**Elements → Event Listeners** tab, or setting a breakpoint inside `handleClick`):
1. **Local Scope:** Variables local to `handleClick`.
2. **Closure (`attachClickListener`):** Retains persistent access to `count` in the heap between clicks.
3. **Global Scope (`Window`):** Outer global environment record.

---

### 🧹 Garbage Collection & `removeEventListener`

Event listeners are heavy because they retain closures over their entire enclosing lexical environment.

| State | Memory Impact | Garbage Collection (GC) |
|---|---|---|
| **Active Listener Attached** | Retains all closed-over outer variables in heap memory | **Not collected** (DOM node holds reference to handler) |
| **Listener Removed** | References to handler and outer scope severed | **Garbage collected** (heap memory reclaimed) |

> ⚠️ **Memory Leak Warning:** As long as a listener remains attached to a DOM node, the JS engine's Garbage Collector cannot free the variables captured in its closure. In SPAs or long-lived apps, unremoved listeners accumulate and cause memory leaks.

> 💡 **Reference Rule:** `removeEventListener()` requires the **exact same function reference**. Anonymous inline callbacks cannot be removed.

```js
// ❌ Memory Leak Risk: Anonymous callback cannot be removed
btn.addEventListener("click", function () {
  console.log("Clicked");
});

// ✅ Best Practice: Named reference enables deterministic cleanup
function handleClick() {
  console.log("Clicked");
}

btn.addEventListener("click", handleClick);

// Clean up when element or component unmounts:
btn.removeEventListener("click", handleClick);
```

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 14. JS Engine Architecture & Google V8

A JavaScript engine is not a physical hardware machine — it is a program (typically written in C++) that executes JS source code by translating it into low-level machine instructions.

### 📦 JavaScript Runtime Environment (JRE)

The engine cannot run in isolation. It requires an enclosing **Runtime Environment**:

```
┌─────────────────────────────────────────────────────────────┐
│              JAVASCRIPT RUNTIME ENVIRONMENT (JRE)           │
│                                                             │
│  ┌──────────────────────────┐    ┌───────────────────────┐  │
│  │        JS ENGINE         │    │  Web APIs (Browser)   │  │
│  │  ┌──────────┐ ┌────────┐ │    │  or C++ APIs (Node)   │  │
│  │  │Heap (Mem)│ │CallStk │ │    │  (timers, DOM, fetch) │  │
│  │  └──────────┘ └────────┘ │    └───────────┬───────────┘  │
│  └─────────────┬────────────┘                │              │
│                │                             │              │
│  ┌─────────────▼────────────┐    ┌───────────▼───────────┐  │
│  │        EVENT LOOP        │◄───┤ Callback / Microtask  │  │
│  │                          │    │ Queues                │  │
│  └──────────────────────────┘    └───────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

| Engine | Host Environment | Creator / Maintainer |
|---|---|---|
| **V8** | Google Chrome, Chromium, Node.js, Brave, Edge | Google |
| **SpiderMonkey** | Mozilla Firefox | Brendan Eich (Netscape / Mozilla) |
| **JavaScriptCore (Nitro)** | Apple Safari | Apple |
| **Chakra** | Internet Explorer / Legacy Edge | Microsoft |

---

### ⚙️ The 3 Engine Execution Phases

Every modern JS engine processes code through three distinct phases:

```
Source Code ──► [ 1. Parsing ] ──► AST ──► [ 2. JIT Compilation ] ──► Bytecode / Machine Code ──► [ 3. Execution ]
```

#### 1. Parsing
- The syntax parser reads the raw text and generates **Tokens** (e.g. `let`, `a`, `=`, `7`).
- Converts tokens into an **Abstract Syntax Tree (AST)** — a hierarchical JSON-like tree defining the program syntax.

#### 2. Compilation — Just-In-Time (JIT)
JavaScript is neither purely interpreted nor purely compiled:
- **Interpreter:** Fast startup; executes code immediately line-by-line, but repeatedly executes loops slowly without optimization.
- **Compiler:** Slow startup (compilation pause before execution), but outputs blazingly fast machine code.
- **JIT Compilation:** Combines both. The interpreter starts executing bytecode instantly, while an optimizing compiler monitors "hot" (frequently called) code and compiles it directly into machine code on the fly.

#### 3. Execution (Google V8 Pipeline)
Inside Google's V8 engine:

| Component | Role | Function |
|---|---|---|
| **Ignition** | Fast Interpreter | Compiles AST directly into **Bytecode** for instant execution |
| **TurboFan** | Optimizing Compiler | Compiles hot bytecode into highly optimized **Machine Code** based on runtime type profiles |
| **De-optimizer** | Type Bailout | If polymorphic types violate compiler assumptions, machine code bails back to Ignition bytecode |
| **Orinoco** | Garbage Collector | Performs concurrent, parallel **Mark-and-Sweep** to clean unreferenced heap memory |

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 15. Trust Issues with setTimeout()

`setTimeout(callback, delay)` does **not** guarantee that the callback executes exactly after `delay` milliseconds.

> ⚠️ **The Golden Rule:** The timer delay specifies the **guaranteed minimum delay** before the callback is placed in the queue, NOT the exact time it will run on the Call Stack.

---

### ⏱️ Why Timers Suffer Delays

When `setTimeout(cb, 5000)` is invoked:
1. The Web API registers the timer and runs the 5000ms countdown in the background.
2. At 5000ms, the Web API pushes `cb` into the **Callback (Task) Queue**.
3. `cb` must wait in the queue until:
   - The **Call Stack** is completely empty (current synchronous script finishes).
   - The **Microtask Queue** is completely drained.
4. If synchronous code blocks the Call Stack for 10 seconds, `cb` waits for the full 10 seconds before executing.

```js
console.log("Start");

setTimeout(function cb() {
  console.log("Callback executed");
}, 5000);

console.log("End");

// Simulate 10 seconds of blocking synchronous work
const startTime = Date.now();
while (Date.now() < startTime + 10000) {
  // Main thread blocked for 10s
}

console.log("Main thread unblocked");

// Output:
// 1. "Start"
// 2. "End"
// 3. "Main thread unblocked" (after 10s)
// 4. "Callback executed"     (ran after 10s, NOT 5s!)
```

---

### ⏳ The `setTimeout(fn, 0)` Pattern

Passing `0ms` does **not** make a callback synchronous:

- The callback is still handed to the Web API timer, pushed to the Callback Queue, and executed only after all top-level synchronous code and microtasks clear.
- **Interview Use Case:** Used to defer non-critical operations, giving the browser's main thread a breather to handle UI re-renders or prioritize immediate user events before the deferred work runs.

```js
console.log("A");

Promise.resolve("resolved").then((val)=> console.log("0 " + val)); // micro-task
setTimeout(() => {  // macro-task
  console.log("B (0ms)");
}, 0);

console.log("C");

// Output: "A" → "C"  → "0 resolved" → "B (0ms)"
```

| Dimension | Synchronous Execution | `setTimeout(fn, 0)` |
|---|---|---|
| **Path** | Runs immediately on Call Stack | Web API → Callback Queue → Event Loop → Call Stack |
| **Execution Timing** | Immediate (current tick) | Deferred to next Macrotask turn (after sync & microtasks) |
| **Main Thread Impact** | Occupies Call Stack | Yields Call Stack, keeps UI responsive |

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 16. Higher-Order Functions & Polyfills

A **Higher-Order Function (HOF)** is any function that fulfills at least one of these two criteria:
1. **Takes one or more functions as arguments** (parameters).
2. **Returns a function** as its result.

The function passed into an HOF as an argument is known as a **Callback Function**.

```js
function x() {
  console.log("hello");
}

function y(x) { // y is the Higher-Order Function, x is the Callback Function
  x();
}

y(x);
```

---

### 🧱 Functional Programming & The DRY Principle

Functional programming emphasizes breaking code into small, pure, reusable units rather than writing monolithic procedural blocks.

#### The Problem: Repetitive Procedural Code (Violating DRY)
Calculating area, circumference, and diameter across an array of radii naively requires repeating 90% of the iteration and memory-allocation logic:

```js
const radius = [3, 1, 2, 4];

// ❌ Repetitive: Each function duplicates the for-loop, output array, and push logic
const calculateArea = function (radius) {
  const output = [];
  for (let i = 0; i < radius.length; i++) {
    output.push(Math.PI * radius[i] * radius[i]);
  }
  return output;
};

const calculateCircumference = function (radius) {
  const output = [];
  for (let i = 0; i < radius.length; i++) {
    output.push(2 * Math.PI * radius[i]);
  }
  return output;
};
```

#### The Solution: Decouple Traversal from Logic (Functional Approach)
Separate the **iteration mechanism** (HOF) from the **business calculation** (pure callback functions):

```js
const radius = [3, 1, 2, 4];

// Pure transformation logic (Single Responsibility)
const area = function (r) {
  return Math.PI * r * r;
};

const circumference = function (r) {
  return 2 * Math.PI * r;
};

const diameter = function (r) {
  return 2 * r;
};

// Generic Higher-Order Function: handles array traversal
const calculate = function (arr, logic) {
  const output = [];
  for (let i = 0; i < arr.length; i++) {
    output.push(logic(arr[i]));
  }
  return output;
};

console.log(calculate(radius, area));          // [ ~28.27, ~3.14, ~12.57, ~50.27 ]
console.log(calculate(radius, circumference)); // [ ~18.85, ~6.28, ~12.57, ~25.13 ]
console.log(calculate(radius, diameter));      // [ 6, 2, 4, 8 ]
```

| Aspect | Procedural Approach | Higher-Order Function Approach |
|---|---|---|
| **DRY Principle** | ❌ Violates DRY (repeats loops & push logic) | ✅ Follows DRY (loop written once) |
| **Separation of Concerns** | Iteration & math coupled together | Iteration separated from mathematical logic |
| **Reusability** | Restricted to one computation | Works with any transformation callback |
| **Testability** | Harder to test isolated formulas | Each callback formula is easily unit-tested |

---

### 🧬 Creating a Polyfill for `Array.prototype.map`

`calculate(radius, area)` mimics the exact behavior of JavaScript’s native `Array.prototype.map()`.

We can turn `calculate` into a true polyfill by attaching it to `Array.prototype`:

```js
// Polyfill for Array.prototype.map
Array.prototype.calculate = function (logic) {
  const output = [];
  // 'this' refers to the array instance calling .calculate()
  for (let i = 0; i < this.length; i++) {
    output.push(logic(this[i]));
  }
  return output;
};

const radius = [3, 1, 2, 4];

console.log(radius.calculate(area)); // Custom prototype method
console.log(radius.map(area));       // Native JS engine method
// Both produce the exact same array!
```

> 💡 **Under the Hood (`this` binding):** When `radius.calculate(area)` executes, `this` inside the prototype function dynamically binds to the `radius` array instance.

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 17. Functional Array Methods — map, filter & reduce

`map`, `filter`, and `reduce` are standard **Higher-Order Functions** built into `Array.prototype`. They iterate over an array immutably (they do not mutate the original array, but return a new array or value).

| Method | Core Purpose | Return Type | Output Length |
|---|---|---|---|
| **`map()`** | Transform every element with a mapping function | New Array | Always identical (`output.length === input.length`) |
| **`filter()`** | Select elements that satisfy a boolean condition | New Array | Variable (`0 <= output.length <= input.length`) |
| **`reduce()`** | Boil down an entire array into a single accumulated result | Any Value (Number, String, Object, Array) | Single accumulated entity |

---

### 🗺️ Array.prototype.map()

Used to transform each element of an array according to a callback function:
- **Callback Signature:** `(currentValue, index, array) => transformedValue`
- **Guarantee:** Never changes the length of the original array; performs a strict 1-to-1 transformation.

```js
const arr = [5, 1, 3, 2, 6];

// Transformation callbacks
function double(x) {
  return 2 * x;
}

function triple(x) {
  return 3 * x;
}

function binary(x) {
  return x.toString(2); // Radix 2 for binary string representation
}

// 1. Passing a named function reference
console.log(arr.map(double)); // [10, 2, 6, 4, 12]
console.log(arr.map(triple)); // [15, 3, 9, 6, 18]
console.log(arr.map(binary)); // ['101', '1', '11', '10', '110']

// 2. Inline arrow function (concise)
console.log(arr.map((x) => x.toString(2)));

// 3. Inline anonymous function statement
console.log(arr.map(function (val) {
  return val.toString(2);
}));
```

---

### 🔍 Array.prototype.filter()

Used to filter an array based on a **predicate function** (a callback returning a truthy or falsy value):
- If the callback returns `true`, the element is included in the new array.
- If `false`, the element is excluded.

```js
const arr = [5, 1, 3, 2, 6];

// Filter elements strictly greater than 4
const greaterThan4 = arr.filter((x) => x > 4);
console.log(greaterThan4); // [5, 6]

// Filter elements strictly less than 3
const lessThan3 = arr.filter((x) => x < 3);
console.log(lessThan3); // [1, 2]

// Filter multiples of 3
const multiplesOf3 = arr.filter((x) => x % 3 === 0);
console.log(multiplesOf3); // [3, 6]
```

---

### 🔄 Array.prototype.reduce()

Used when you need to iterate through an array and aggregate or accumulate its elements into a **single output** (such as a sum, maximum value, grouped object, or flattened array).

#### Method Signature & Anatomy
```js
arr.reduce(function (accumulator, currentValue, index, array) {
  // return updated accumulator
}, initialValue);
```

- **`accumulator` (`acc`)**: Stores the accumulated result from previous iterations. On iteration 1, it equals `initialValue`.
- **`currentValue` (`curr`)**: The current array element being processed.
- **`initialValue`**: The starting value passed to the accumulator. *(Always pass an explicit initial value to avoid edge cases on empty arrays!)*

#### 1. Sum of an Array
```js
const arr = [5, 1, 3, 2, 6];

const sum = arr.reduce(function (acc, curr) {
  acc += curr;
  return acc;
}, 0);

console.log(sum); // 17
```

**Accumulator Trace Table:**

| Iteration | `acc` (Start of step) | `curr` | `acc + curr` | Returned to next iteration |
|---|---|---|---|---|
| Step 1 | `0` *(initialValue)* | `5` | `0 + 5 = 5` | `5` |
| Step 2 | `5` | `1` | `5 + 1 = 6` | `6` |
| Step 3 | `6` | `3` | `6 + 3 = 9` | `9` |
| Step 4 | `9` | `2` | `9 + 2 = 11` | `11` |
| Step 5 | `11` | `6` | `11 + 6 = 17` | **Final Return: `17`** |

#### 2. Finding the Maximum Value
```js
const maxVal = arr.reduce(function (max, curr) {
  if (curr > max) {
    max = curr;
  }
  return max;
}, 0);

console.log(maxVal); // 6
```

---

### ⚡ Practical Scenarios & Method Chaining

Working with complex data structures (objects) in real-world applications:

```js
const data = [
  { firstName: "decider", secondName: "2002", age: 25 },
  { firstName: "dead", secondName: "pool", age: 46 },
  { firstName: "ken", secondName: "miles", age: 50 },
  { firstName: "cristiano", secondName: "ronaldo", age: 46 }
];
```

#### 1. Transform Objects to Array of Strings (`map`)
```js
// List of full names
const fullNames = data.map((x) => `${x.firstName} ${x.secondName}`);
console.log(fullNames);
// ['decider 2002', 'dead pool', 'ken miles', 'cristiano ronaldo']
```

#### 2. Frequency Map / Grouping by Property (`reduce`)
Tally counts of distinct properties into an accumulator object:

```js
// Count people by age: { 25: 1, 46: 2, 50: 1 }
const ageTally = data.reduce(function (acc, curr) {
  if (!acc[curr.age]) {
    acc[curr.age] = 1;
  } else {
    acc[curr.age] = ++acc[curr.age];
  }
  return acc;
}, {});

console.log(ageTally); // { 25: 1, 46: 2, 50: 1 }
```

#### 3. Method Chaining (`filter` + `map`)
Find first names of people whose age is strictly greater than 30:

```js
const over30Names = data
  .filter((x) => x.age > 30)
  .map((x) => x.firstName);

console.log(over30Names); // ['dead', 'ken', 'cristiano']
```

#### 4. Pro Interview Pattern: Single-Pass `filter` + `map` via `reduce`
Instead of chaining `.filter().map()` (which traverses the array twice and creates an intermediate array in memory), use `reduce` with an empty array `[]` accumulator to filter and extract in a **single $O(N)$ pass**:

```js
// People with age < 50: single-pass filter + projection
const under50Names = data.reduce(function (acc, curr) {
  if (curr.age < 50) {
    acc.push(curr.firstName); // Filters and maps simultaneously
  }
  return acc;
}, []);

console.log(under50Names); // ['decider', 'dead', 'cristiano']
```

> 💡 **Performance Note:** Chaining `.filter().map()` creates an intermediate array in heap memory between passes. In performance-critical hot loops with large datasets, a single `reduce` pass is more cache-friendly and avoids extra heap allocations.

<p align="right">(<a href="#top">back to top</a>)
<hr/>


## 18. Callback Pitfalls — Callback Hell & Inversion of Control

Callbacks are fundamental to JavaScript’s asynchronous execution model, allowing the single main thread to offload tasks to Web APIs. However, relying on callbacks for complex asynchronous workflows exposes two major architectural flaws: **Callback Hell** and **Inversion of Control**.

| Pitfall | Core Nature | Technical Risk | Solution |
|---|---|---|---|
| **Callback Hell** | Code structure / readability issue | Deeply nested, unmaintainable horizontal pyramid (**Pyramid of Doom**) | Promise Chaining |
| **Inversion of Control** | Authority / reliability flaw | Blindly trusting external/3rd-party code with execution authority | Native Promises |

---

### 🔥 1. Callback Hell (The Pyramid of Doom)

When asynchronous tasks have sequential dependencies (e.g., placing an order → processing payment → generating summary → updating wallet), nesting callbacks inside callbacks causes the code to grow horizontally instead of vertically.

```js
// E-commerce checkout flow via nested callbacks
const cart = ["shoes", "pants", "kurta"];

api.createOrder(cart, function (orderId) {
  api.proceedToPayment(orderId, function (paymentInfo) {
    api.showOrderSummary(paymentInfo, function (summary) {
      api.updateWallet(summary, function () {
        console.log("Wallet updated successfully");
      });
    });
  });
});
```

- **Visual Shape:** Known as the **Pyramid of Doom** (unmaintainable `})` trailing closing tags).
- **Problems:**
  - Highly brittle and difficult to debug or refactor.
  - Exception handling requires boilerplate error checks at every single nesting level.
  - Breaches code readability and maintainability.

---

### 🎛️ 2. Inversion of Control (The Fatal Flaw)

**Inversion of Control (IoC)** is far more dangerous than Callback Hell:
> When we pass a callback function to another function, we **surrender control** over our code's execution to that receiving function.

```js
api.createOrder(cart, function () {
  api.proceedToPayment(); // We handed over control of payment to createOrder!
});
```

#### Why Inversion of Control is Dangerous:
1. **Blind Trust:** You assume `createOrder` will faithfully execute `proceedToPayment()`. But `createOrder` could be an external npm package or written by another team.
2. **Double/Multiple Invocations:** If `createOrder` has an internal bug or retry loop, it might invoke `proceedToPayment()` **twice**, charging the customer twice.
3. **Zero Invocations:** If an unhandled error occurs internally inside `createOrder`, your callback may **never be called at all**, silently dropping the user transaction.
4. **Altered Timing:** The callback might be invoked synchronously instead of asynchronously, altering expected execution flow.

> ⚠️ **The Core Problem:** You are no longer in control of when, how many times, or if your critical code runs.

---

### 🌉 The Bridge to Promises

ES6 **Promises** were designed specifically to eliminate both pitfalls:
- **Solves Inversion of Control:** Instead of *passing* our callback into an untrusted function, the function *returns an immutable Promise object*. We attach our handler using `.then()`. The Promise guarantees our callback is called **exactly once**, only upon completion, and never mutated.
- **Solves Callback Hell:** Flattens nested pyramids into a clean, vertical **Promise Chain**.

<p align="right">(<a href="#top">back to top</a>)
<hr/>

## 19. Quick Summary Table

| Concept | Key Takeaway |
|---|---|
| Execution Context | Memory phase → Code phase |
| `var` hoisting | `undefined` |
| `let`/`const` hoisting | TDZ → `ReferenceError` if accessed early |
| Function Declaration | Fully hoisted — callable before declaration |
| Function Expression / Arrow | `undefined` → `TypeError` if called early |
| First-Class Functions | Functions treated as values (pass, return, assign) |
| Callback Function | Function passed as argument; enables async non-blocking execution |
| Higher-Order Function (HOF) | Function that accepts another function as argument or returns one |
| Functional Programming (DRY) | Decouple iteration/traversal logic from business calculations |
| Map Polyfill (`Array.prototype`) | Custom array method using `this` to access array elements and apply callback |
| `Array.prototype.map()` | Transforms every element 1:1; output array length always matches input |
| `Array.prototype.filter()` | Selects subset of elements satisfying a boolean predicate condition |
| `Array.prototype.reduce()` | Aggregates array elements into a single accumulator value (number, object, or array) |
| Callback Hell | Deeply nested callbacks forming a "Pyramid of Doom"; brittle and unmaintainable |
| Inversion of Control (IoC) | Surrendering execution authority of callbacks to external functions (trust issue) |
| Event Listener Cleanup | Handlers retain closures in heap; remove with `removeEventListener` to prevent memory leaks |
| Web APIs | Browser features outside JS engine (`setTimeout`, DOM, `fetch`, `console`) exposed on `window` |
| Queue Starvation | Continuous microtasks block macrotasks/UI from ever executing |
| V8 Engine Pipeline | AST → Ignition (Bytecode) ↔ TurboFan (Optimized Machine Code) |
| JIT Compilation | Combines interpreter speed at startup with compiler optimizations during runtime |
| `setTimeout` Trust Issues | Delay is minimum wait time before queuing; blocked Call Stack postpones execution |
| `setTimeout(fn, 0)` | Defers callback to next macrotask turn; does not execute synchronously |
| Call Stack | LIFO — manages execution context order |
| `this` at global scope | `window` (browser) / `global` (Node) |
| `undefined` | Declared, not yet assigned |
| `not defined` | Never declared → `ReferenceError` |
| Lexical Environment | Local memory + parent reference chain |
| Scope Chain | Walk parent refs until variable found or null |
| Closure | Inner fn retains outer lexical env after outer returns |
| Microtask Queue | Runs before Macrotask (Promises, `MutationObserver`) |
| Macrotask Queue | Runs after microtasks clear (`setTimeout`, I/O, DOM events) |

<p align="right">(<a href="#top">back to top</a>)
<hr/>
