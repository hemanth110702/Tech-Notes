# JavaScript — Interview Quick Reference

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

---

## 10. Event Loop & Async Model

```
Call Stack → (empty?) → drain Microtask Queue → pick next Macrotask → repeat
```

| Component | Role | Examples |
|---|---|---|
| **Call Stack** | Executes JS synchronously | All sync code |
| **Web APIs / libuv** | Handles async tasks off-thread | fetch, timers, I/O |
| **Microtask Queue** | High-priority; runs before macrotasks | `Promise.then`, `queueMicrotask` |
| **Macrotask Queue** | Lower-priority | `setTimeout`, `setInterval`, I/O callbacks |

**Golden Rule:** The Event Loop empties the **entire Microtask Queue** before picking the next Macrotask.

```js
console.log("1");
setTimeout(() => console.log("2"), 0);        // Macrotask
Promise.resolve().then(() => console.log("3")); // Microtask
console.log("4");
// Output: 1 → 4 → 3 → 2
```

---

## 11. Quick Summary Table

| Concept | Key Takeaway |
|---|---|
| Execution Context | Memory phase → Code phase |
| `var` hoisting | `undefined` |
| `let`/`const` hoisting | TDZ → `ReferenceError` if accessed early |
| Function Declaration | Fully hoisted — callable before declaration |
| Function Expression / Arrow | `undefined` → `TypeError` if called early |
| Call Stack | LIFO — manages execution context order |
| `this` at global scope | `window` (browser) / `global` (Node) |
| `undefined` | Declared, not yet assigned |
| `not defined` | Never declared → `ReferenceError` |
| Lexical Environment | Local memory + parent reference chain |
| Scope Chain | Walk parent refs until variable found or null |
| Closure | Inner fn retains outer lexical env after outer returns |
| Microtask Queue | Runs before Macrotask (Promises) |
| Macrotask Queue | Runs after microtasks clear (setTimeout) |
