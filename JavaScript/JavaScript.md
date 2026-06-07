# JavaScript Course — Study Notes

A complete reference for every topic covered in this course -
📚 Watch the course here: https://youtu.be/EerdGm-ehJQ

---

## Table of Contents

1. [Lesson 1 — JavaScript Basics](#lesson-1--javascript-basics)
2. [Lesson 2 — Numbers & Math](#lesson-2--numbers--math)
3. [Lesson 3 — Strings](#lesson-3--strings)
4. [Lesson 4 — HTML & CSS Review](#lesson-4--html--css-review)
5. [Lesson 5 — Variables](#lesson-5--variables)
6. [Lesson 6 — Booleans & Conditionals](#lesson-6--booleans--conditionals)
7. [Lesson 7 — Functions](#lesson-7--functions)
8. [Lesson 8 — Objects](#lesson-8--objects)
9. [Lesson 9 — The DOM](#lesson-9--the-dom)
10. [Lesson 10 — DOM Projects](#lesson-10--dom-projects)
11. [Lesson 11 — Arrays & Loops](#lesson-11--arrays--loops)
12. [Lesson 12 — Advanced Functions](#lesson-12--advanced-functions)
13. [Lesson 13 — Building an Amazon Clone](#lesson-13--building-an-amazon-clone)
14. [Lesson 14 — Checkout Page](#lesson-14--checkout-page)
15. [Lesson 15 — ES Modules](#lesson-15--es-modules)
16. [Lesson 16 — External Libraries & Dates](#lesson-16--external-libraries--dates)
17. [Lesson 17 — Automated Testing](#lesson-17--automated-testing)
18. [Lesson 18 — OOP & Backend Basics](#lesson-18--oop--backend-basics)
19. [Lesson 19 — Backend, Callbacks, Promises & Async/Await](#lesson-19--backend-callbacks-promises--asyncawait)

---

## Lesson 1 — JavaScript Basics

**Files:** `lesson-01/javascript-basics.js`

JavaScript runs inside a browser. You can display things with `alert()`, interact with the page via `document`, and run arithmetic directly.

```js
alert("hello"); // popup dialog
alert("Good job!");

2 + 2; // evaluated but not displayed
10 - 3;

document.body.innerHTML = "hello"; // changes page content
```

**Key points:**

- `alert()` shows a browser popup.
- `document.body.innerHTML` sets the entire body content as HTML.
- JS expressions evaluate but you need `console.log()` or `alert()` to see the result.

---

## Lesson 2 — Numbers & Math

**Files:** `lesson-02/numbers-and-math.js`

### Basic arithmetic

```js
2 + 2; // 4
10 - 3; // 7
10 * 3; // 30
10 / 2; // 5
```

### Order of operations (PEMDAS/BODMAS)

```js
1 +
  1 *
    3(
      // 4  (multiplication first)
      1 + 1,
    ) *
    3; // 6  (parentheses first)
```

### Float inaccuracies

Floating-point numbers are stored in binary and can be slightly imprecise:

```js
0.1 + 0.2; // 0.30000000000000004  ← imprecise!
20.95 +
  7.99(
    // also slightly off

    // Fix: work in cents (integers), then divide
    2095 + 799,
  ) /
    100; // 28.94 ← exact
```

### Rounding

```js
Math.round(2.2); // 2
Math.round(2.8); // 3

Math.round((2095 + 799) * 0.1) / 100; // rounds tax to nearest cent
```

---

## Lesson 3 — Strings

**Files:** `lesson-03/strings.js`

### String basics

```js
"hello";
"some" + "text"; // "sometext"  (concatenation)
"some" + "more" + "text";

typeof 2; // "number"
typeof "hello"; // "string"
```

### Mixing strings and numbers

```js
"hello" + 3; // "hello3"  (number converted to string)
"$" + 20.95 + 7.99; // "$20.957.99"  ← wrong! strings concatenate left-to-right
"$" + (20.95 + 7.99); // "$28.94"  ← correct, parentheses force math first
```

### Quote types

```js
"hello"; // double quotes — same as single
"I'm learning JavaScript"; // double quotes let you use apostrophes freely
'I\'m learning JavaScript'; // single quotes need escape (\')
alert("some\ntext"); // \n = newline
```

### Template literals (backticks)

The modern, readable way to embed expressions in strings:

```js
`hello``Items (${1 + 1}): $${(2095 + 799) / 100}` // "Items (2): $28.94"
`some
text`; // multi-line strings work natively in template literals
```

**Key rule:** Use `${}` inside backtick strings to embed any JS expression.

---

## Lesson 4 — HTML & CSS Review

**Files:** `04-website.html`

Quick review of how HTML, CSS, and JS work together.

```html
<!-- HTML comment -->
<button class="red-button" onclick="alert('Good job!');">hello</button>

<style>
  /* CSS comment */
  .red-button {
    background-color: red;
    color: white;
    border: none;
  }
</style>

<script>
  // Single-line JS comment
  /* Multi-line
     JS comment */
  console.log(2 + 2); // logs to browser console
  console.log("some" + "text");
</script>
```

**Key points:**

- `onclick="..."` runs JS when a button is clicked.
- `console.log()` prints to the browser's DevTools console (not the page).
- CSS classes are applied with `class=""` and styled with `.className {}`.

---

## Lesson 5 — Variables

**Files:** `05-variables.html`

Variables store values so you can reuse and update them.

```js
let variable1 = 3;
console.log(variable1); // 3

const calculation = 2 + 2;
console.log(calculation); // 4
console.log(calculation + 2); // 6

const message = "hello";
console.log(message); // "hello"

// Reassigning a let variable
variable1 = 5;
console.log(variable1); // 5

variable1 = variable1 + 1;
console.log(variable1); // 6
```

### `let` vs `const` vs `var`

| Keyword | Can reassign? | Notes                                            |
| ------- | ------------- | ------------------------------------------------ |
| `const` | No            | Use by default; prevents accidental reassignment |
| `let`   | Yes           | Use when the value needs to change               |
| `var`   | Yes           | Old style — avoid in modern JS                   |

---

## Lesson 6 — Booleans & Conditionals

**Files:** `06-booleans.html`, `06-rock-paper-scissors.html`

### Booleans

```js
true;
false;

console.log(3 > 5 - 5); // true  (3 > 0)
console.log(5 === "5.00"); // false (strict equality: type matters)
```

### if / else if / else

```js
const age = 15;

if (age >= 16) {
  console.log("You can drive");
} else if (age >= 14) {
  console.log("Almost there!");
} else {
  console.log("You can not drive");
}
```

### Logical operators

```js
console.log(true && false); // false  (AND — both must be true)
console.log(true || false); // true   (OR — at least one must be true)
console.log(!false); // true   (NOT — flips the boolean)
```

### Truthy & Falsy

In JavaScript, non-boolean values are coerced to booleans in conditions:

```js
// Falsy values: 0, '', null, undefined, NaN, false
// Everything else is truthy

if (0) { ... }          // never runs — 0 is falsy
if (cartQuantity) { ... } // runs if quantity is not 0

console.log(!0)         // true
console.log('text' / 5) // NaN — result of invalid math
```

### Ternary operator

```js
const result = 0 ? "truthy" : "falsy"; // 'falsy'
// condition ? valueIfTrue : valueIfFalse
```

### Short-circuit operators

```js
false && console.log("hello"); // 'hello' never logs — short-circuits
5 && "hello"; // returns 'hello' (last truthy value)
undefined || "USD"; // returns 'USD' (fallback for falsy)
```

---

## Lesson 7 — Functions

**Files:** `07-functions.html`, `07-rock-paper-scissors.html`

Functions let you group reusable code.

### Basic function

```js
function function1() {
  console.log("hello");
  console.log(2 + 2);
}

function1(); // call it once
function1(); // call it again
```

### Parameters & return values

```js
function calculateTax(cost, taxPercent = 0.1) {
  // 0.1 is a default parameter
  console.log(cost * taxPercent);
}

calculateTax(2000, 0.2); // 400  (custom taxPercent)
calculateTax(5000); // 500  (uses default 0.1)
```

**Key points:**

- Parameters are the names inside `function foo(param1, param2)`.
- Default parameters kick in when the caller doesn't provide a value.
- Use `return value;` to send a result back to the caller.

---

## Lesson 8 — Objects

**Files:** `08-objects.html`

Objects group related data and behaviour together.

### Creating and accessing objects

```js
const product = {
  name: "socks",
  price: 1090,
};

console.log(product.name); // "socks"   — dot notation
console.log(product["name"]); // "socks"   — bracket notation (same result)
product.name = "cotton socks"; // update a property
product.newProperty = true; // add a new property
delete product.newProperty; // remove a property
```

### Nested objects & methods

```js
const product2 = {
  name: "shirt",
  "delivery-time": "1 day", // hyphenated keys need quotes
  rating: {
    stars: 4.5,
    count: 87,
  },
  fun: function () {
    console.log("function inside object");
  },
};

console.log(product2.rating.count); // 87
console.log(product2["delivery-time"]); // "1 day"  (must use brackets)
product2.fun(); // "function inside object"
```

### JSON

```js
const jsonString = JSON.stringify(product2); // object → JSON string
console.log(JSON.parse(jsonString)); // JSON string → object
```

### Object references

Objects are assigned by reference, not by value:

```js
const object1 = { message: "hello", price: 799 };
const object2 = object1; // both point to the same object

object1.message = "Good job!";
console.log(object2.message); // "Good job!" — object2 also changed!

const object3 = { message: "Good job!", price: 799 };
console.log(object1 === object3); // false — different objects in memory
```

### Destructuring

```js
const { message, price: cost } = object1;
// Pulls out 'message' and renames 'price' to 'cost'
console.log(message); // "Good job!"
console.log(cost); // 799
```

### Shorthand property & method syntax

```js
const message = "hello";

const object4 = {
  message, // shorthand for message: message
  method() {
    // shorthand for method: function() {}
    // ...
  },
};
```

### Built-in string methods (strings are objects too)

```js
Auto-Boxing
console.log("hello".length); // 5
console.log("hello".toUpperCase()); // "HELLO"
```

---

## Lesson 9 — The DOM

**Files:** `09-dom.html`, `09-rock-paper-scissors.html`

The DOM (Document Object Model) lets JS read and change the HTML page.

```js
// Read content
console.log(document.querySelector("button").innerHTML); // "hello"

// Change content
document.querySelector("button").innerHTML = "Changed";

// Select by class name
const buttonElement = document.querySelector(".js-button");

// Change the page title
document.title = "Changed";

// Replace the entire body
document.body.innerHTML = "<button>Good job!</button>";
```

**Key points:**

- `document.querySelector(selector)` returns the **first** matching element.
- `.innerHTML` gets or sets the HTML inside an element.
- Use CSS selectors: `'button'` for tags, `'.className'` for classes.

---

## Lesson 10 — DOM Projects

**Files:** `10-dom-projects.html`

Real projects combining DOM manipulation, events, and type conversion.

### Type conversion

```js
console.log("25" - 5); // 20  — JS converts string '25' to number for subtraction
console.log("25" + 5); // "255" — + triggers string concatenation!

Number("25"); // 25  (explicit conversion)
String(25); // "25"
```

### The window object

```js
window.document; // same as just `document`
window.console.log("window"); // same as console.log
window.alert; // same as alert
```

### Subscribe button project

```js
function subscribe() {
  const buttonElement = document.querySelector(".js-subscribe-button");

  if (buttonElement.innerText === "Subscribe") {
    buttonElement.innerHTML = "Subscribed";
    buttonElement.classList.add("is-subscribed"); // add CSS class
  } else {
    buttonElement.innerHTML = "Subscribe";
    buttonElement.classList.remove("is-subscribed"); // remove CSS class
  }
}
```

### Keyboard event & shipping calculator

```js
function handleCostKeydown(event) {
  if (event.key === "Enter") {
    // detect Enter key
    calculateTotal();
  }
}

function calculateTotal() {
  const inputElement = document.querySelector(".js-cost-input");
  let cost = Number(inputElement.value); // get value from input, convert to number

  if (cost < 40) {
    cost = cost + 10; // add shipping
  }

  document.querySelector(".js-total-cost").innerHTML = `$${cost}`;
}
```

---

## Lesson 11 — Arrays & Loops

**Files:** `11-arrays-and-loops.html`, `11-todo-list.html`

### Arrays

```js
const myArray = [10, 20, 30];

console.log(myArray[1]); // 20  (zero-indexed)
myArray[0] = 99; // update a value

// Arrays can hold mixed types
[1, "hello", true, { name: "socks" }, [1, 2]];

console.log(typeof [1, 2]); // "object"
console.log(Array.isArray([1, 2])); // true

myArray.push(100); // add to end
myArray.splice(0, 1); // remove 1 element starting at index 0
console.log(myArray.length); // number of items

const array2 = array1.slice(); // shallow copy (not a reference)
```

### Array destructuring

```js
const [firstValue, secondValue] = [1, 2, 3];
// firstValue = 1, secondValue = 2
```

### while loop

```js
let i = 1;
while (i <= 5) {
  console.log(i);
  i++;
}
```

### for loop

```js
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
```

### Looping through an array

```js
const todoList = ["make dinner", "wash dishes", "watch youtube"];

for (let i = 0; i < todoList.length; i++) {
  const value = todoList[i];
  console.log(value);
}
```

### break and continue

```js
for (let i = 1; i <= 10; i++) {
  if (i % 3 === 0) {
    continue; // skip multiples of 3
  }
  console.log(i);
  if (i === 8) {
    break; // stop the loop entirely
  }
}
```

### Returning early from a function

```js
function doubleArray(nums) {
  const numsDoubled = [];
  for (let i = 0; i < nums.length; i++) {
    const num = nums[i];
    if (num === 0) {
      return numsDoubled; // early exit when 0 is found
    }
    numsDoubled.push(num * 2);
  }
  return numsDoubled;
}
```

---

## Lesson 12 — Advanced Functions

**Files:** `12-advanced-functions.html`, `12-rock-paper-scissors.html`, `12-todo-list.html`

### Functions are values

```js
const function1 = function () {
  console.log("hello");
};
console.log(typeof function1); // "function"
function1();
```

### Passing functions as arguments (callbacks)

```js
function run(param) {
  param(); // calls the function passed in
}

run(function () {
  console.log("hello4");
});
```

### setTimeout & setInterval

```js
setTimeout(function () {
  console.log("timeout");
}, 3000); // runs once after 3 seconds

setInterval(function () {
  console.log("interval");
}, 3000); // runs every 3 seconds

console.log("next line"); // runs immediately, before the timeout fires
```

### Arrow functions

```js
// Regular function expression
const regularFunction = function (param) {
  return param + 1;
};

// Arrow function — same thing, shorter syntax
const arrowFunction = (param) => {
  return param + 1;
};

// One parameter — can drop parentheses
const oneParam = (param) => {
  console.log(param + 1);
};

// One-line body — can drop braces and return keyword
const oneLine = () => 2 + 3;
console.log(oneLine()); // 5
```

### forEach

```js
["make dinner", "wash dishes", "watch youtube"].forEach((value, index) => {
  if (value === "wash dishes") {
    return; // skip this iteration (like continue)
  }
  console.log(index, value);
});
```

### filter

Returns a new array with only elements that pass the test:

```js
console.log([1, -3, 5].filter((value) => value >= 0));
// [1, 5]
```

### map

Returns a new array where every element is transformed:

```js
console.log([1, 1, 3].map((value) => value * 2));
// [2, 2, 6]
```

### Event listeners

```js
const buttonElement = document.querySelector(".js-button");

// Named function — can be removed later
const eventListener = () => {
  console.log("click");
};
buttonElement.addEventListener("click", eventListener);
buttonElement.removeEventListener("click", eventListener);

// Anonymous arrow — can't be removed
buttonElement.addEventListener("click", () => {
  console.log("click2");
});
```

### Function hoisting

```js
greeting();   // works even though the function is defined below!

function greeting() {
  console.log('hello');
}

// Function expressions are NOT hoisted:
const func = function() { ... };  // must be defined before calling
```

### localStorage

```js
// Save data that persists across page reloads
localStorage.setItem("score", JSON.stringify({ wins: 0, losses: 0, ties: 0 }));

// Read it back
const score = JSON.parse(localStorage.getItem("score"));
// If nothing is saved yet, getItem returns null — use || for a fallback:
const score = JSON.parse(localStorage.getItem("score")) || {
  wins: 0,
  losses: 0,
  ties: 0,
};
```

### Keyboard events on document.body

```js
document.body.addEventListener("keydown", (event) => {
  if (event.key === "r") playGame("rock");
  else if (event.key === "p") playGame("paper");
  else if (event.key === "s") playGame("scissors");
});
```

---

## Lesson 13 — Building an Amazon Clone

**Files:** `lesson-13/scripts/amazon.js`, `lesson-13/data/`

### Generating dynamic HTML

```js
let productsHTML = "";

products.forEach((product) => {
  productsHTML += `
    <div class="product-container">
      <div class="product-name">${product.name}</div>
      <div class="product-price">$${(product.priceCents / 100).toFixed(2)}</div>
      <button class="js-add-to-cart" data-product-id="${product.id}">
        Add to Cart
      </button>
    </div>
  `;
});

document.querySelector(".js-products-grid").innerHTML = productsHTML;
```

### data attributes & dataset

```html
<button data-product-id="abc123">Add to Cart</button>
```

```js
const productId = button.dataset.productId; // "abc123"
```

### Event delegation pattern

```js
document.querySelectorAll(".js-add-to-cart").forEach((button) => {
  button.addEventListener("click", () => {
    const productId = button.dataset.productId;

    let matchingItem;
    cart.forEach((item) => {
      if (productId === item.productId) {
        matchingItem = item;
      }
    });

    if (matchingItem) {
      matchingItem.quantity += 1;
    } else {
      cart.push({ productId, quantity: 1 });
    }

    // Recalculate total cart count
    let cartQuantity = 0;
    cart.forEach((item) => {
      cartQuantity += item.quantity;
    });
    document.querySelector(".js-cart-quantity").innerHTML = cartQuantity;
  });
});
```

---

## Lesson 14 — Checkout Page

**Files:** `lesson-14/`

Builds the checkout and payment summary pages of the Amazon clone by:

- Rendering cart items with delete/update functionality.
- Calculating and displaying order totals.
- Building a multi-page app (amazon.html → checkout.html → orders.html).

Key patterns: same DOM rendering approach as Lesson 13, but split across multiple pages with shared data via `localStorage`.

---

## Lesson 15 — ES Modules

**Files:** `lesson-15/scripts/amazon.js`

ES Modules let you split code into separate files.

### Exporting

```js
// data/cart.js
export const cart = [];

export function addToCart(productId) { ... }
```

### Importing

```js
// scripts/amazon.js
import { cart, addToCart } from "../data/cart.js";
import { products } from "../data/products.js";
import { formatCurrency } from "./utils/money.js";
```

### Named vs default export

```js
// Named export (can have multiple per file)
export function formatCurrency(priceCents) {
  return (Math.round(priceCents) / 100).toFixed(2);
}

// Default export (one per file)
export default formatCurrency;
```

```js
// Importing default
import formatCurrency from "./utils/money.js";
// Importing named
import { formatCurrency } from "./utils/money.js";
```

**Key point:** Add `type="module"` to your script tag to use ES Modules in a browser:

```html
<script type="module" src="scripts/amazon.js"></script>
```

---

## Lesson 16 — External Libraries & Dates

**Files:** `lesson-16/scripts/checkout/orderSummary.js`

### Importing from a CDN (external package)

```js
import { hello } from "https://unpkg.com/supersimpledev@1.0.1/hello.esm.js";
import dayjs from "https://unpkg.com/supersimpledev@8.5.0/dayjs/esm/index.js";
```

### dayjs — date manipulation

```js
const today = dayjs();
const deliveryDate = today.add(7, "days");
const dateString = deliveryDate.format("dddd, MMMM D");
// e.g. "Saturday, June 14"
```

### Conditional delivery price display

```js
const priceString =
  deliveryOption.priceCents === 0
    ? "FREE"
    : `$${formatCurrency(deliveryOption.priceCents)} -`;
```

---

## Lesson 17 — Automated Testing

**Files:** `lesson-17/tests/`

Uses the **Jasmine** testing framework.

### Test structure

```js
describe("test suite: formatCurrency", () => {
  it("converts cents into dollars", () => {
    expect(formatCurrency(2095)).toEqual("20.95");
  });

  it("works with 0", () => {
    expect(formatCurrency(0)).toEqual("0.00");
  });

  it("rounds up to the nearest cent", () => {
    expect(formatCurrency(2000.5)).toEqual("20.01");
  });
});
```

### Setup with beforeEach

```js
describe("test suite: renderOrderSummary", () => {
  beforeEach(() => {
    // runs before each `it` block
    document.querySelector(".js-test-container").innerHTML = `
      <div class="js-order-summary"></div>
      <div class="js-payment-summary"></div>
    `;

    // Mock localStorage so tests don't depend on real storage
    spyOn(localStorage, "getItem").and.callFake(() => {
      return JSON.stringify([
        { productId: "abc", quantity: 2, deliveryOptionId: "1" },
      ]);
    });
    spyOn(localStorage, "setItem");

    loadFromStorage();
    renderOrderSummary();
  });

  it("displays the cart", () => {
    expect(document.querySelectorAll(".js-cart-item-container").length).toEqual(
      2,
    );
  });

  it("removes a product", () => {
    document.querySelector(".js-delete-link-abc").click();
    expect(document.querySelectorAll(".js-cart-item-container").length).toEqual(
      1,
    );
  });
});
```

**Key concepts:**

- `describe()` groups related tests.
- `it()` defines a single test case.
- `expect(actual).toEqual(expected)` is an assertion.
- `beforeEach()` runs setup code before every test.
- `spyOn()` intercepts a function call (mocking).

---

## Lesson 18 — OOP & Backend Basics

**Files:** `lesson-18/data/cart-oop.js`, `lesson-18/data/cart-class.js`, `lesson-18/data/backend-practice.js`

### Constructor function pattern (old style)

```js
function Cart(localStorageKey) {
  const cart = {
    cartItems: undefined,

    loadFromStorage() {
      this.cartItems = JSON.parse(localStorage.getItem(localStorageKey));
    },
    saveToStorage() {
      localStorage.setItem(localStorageKey, JSON.stringify(this.cartItems));
    },
    addToCart(productId) { ... },
    removeFromCart(productId) { ... }
  };
  return cart;
}

const cart = Cart('cart-oop');
cart.loadFromStorage();
```

### Class syntax (modern style)

```js
class Cart {
  cartItems;
  #localStorageKey; // # makes it a private field — only accessible inside the class

  constructor(localStorageKey) {
    this.#localStorageKey = localStorageKey;
    this.#loadFromStorage();
  }

  #loadFromStorage() {
    // private method
    this.cartItems = JSON.parse(localStorage.getItem(this.#localStorageKey));
    if (!this.cartItems) {
      this.cartItems = [];
    }
  }

  saveToStorage() {
    localStorage.setItem(this.#localStorageKey, JSON.stringify(this.cartItems));
  }

  addToCart(productId) {
    let matchingItem;
    this.cartItems.forEach((item) => {
      if (productId === item.productId) matchingItem = item;
    });
    if (matchingItem) {
      matchingItem.quantity += 1;
    } else {
      this.cartItems.push({ productId, quantity: 1, deliveryOptionId: "1" });
    }
    this.saveToStorage();
  }

  removeFromCart(productId) {
    this.cartItems = this.cartItems.filter(
      (item) => item.productId !== productId,
    );
    this.saveToStorage();
  }
}

const cart = new Cart("cart-oop");
const businessCart = new Cart("cart-business");

console.log(cart instanceof Cart); // true — instanceof checks the class
```

### Backend basics — XHR request

```js
const xhr = new XMLHttpRequest();

xhr.addEventListener("load", () => {
  console.log(xhr.response); // data from the server
});

xhr.open("GET", "https://supersimplebackend.dev");
xhr.send();
```

**Key OOP concepts:**

- `class` defines a blueprint for objects.
- `constructor()` runs when you call `new ClassName()`.
- `this` refers to the current instance.
- `#field` is a private field — cannot be accessed from outside the class.
- `instanceof` checks whether an object was created from a given class.

### Inheritance — `extends` & `super`

A child class inherits all properties and methods of its parent, and can add or override its own.

```js
class Product {
  id;
  image;
  name;
  rating;
  priceCents;

  constructor(productDetails) {
    this.id = productDetails.id;
    this.image = productDetails.image;
    this.name = productDetails.name;
    this.rating = productDetails.rating;
    this.priceCents = productDetails.priceCents;
  }

  getStarsUrl() {
    return `images/ratings/rating-${this.rating.stars * 10}.png`;
  }

  getPrice() {
    return `$${formatCurrency(this.priceCents)}`;
  }

  extraInfoHTML() {
    return ""; // default: no extra info
  }
}

class Clothing extends Product {
  sizeChartLink;

  constructor(productDetails) {
    super(productDetails); // call the parent constructor first
    this.sizeChartLink = productDetails.sizeChartLink;
  }

  extraInfoHTML() {
    // override the parent method
    return `
      <a href="${this.sizeChartLink}" target="_blank">Size chart</a>
    `;
  }
}
```

**Key points:**

- `extends` makes `Clothing` a subclass of `Product`.
- `super(productDetails)` calls `Product`'s constructor — required before using `this`.
- Overriding `extraInfoHTML()` is **polymorphism** — the same method name behaves differently per class.

### Polymorphism — same method, different behaviour

Because both `Product` and `Clothing` have `extraInfoHTML()`, you can call it on any product without checking the type:

```js
products.forEach((product) => {
  productsHTML += `
    <div>
      ${product.getPrice()}
      ${product.extraInfoHTML()}  <!-- returns '' for Product, size chart link for Clothing -->
    </div>
  `;
});
```

### Discriminator property — choosing the right class

Use a `type` field in data to decide which class to create:

```js
products = productsData.map((productDetails) => {
  if (productDetails.type === "clothing") {
    return new Clothing(productDetails);
  }
  return new Product(productDetails);
});
```

### `this` — context details

`this` changes depending on **where** the function is called:

```js
// At the top level, `this` is the window object
console.log(this); // Window {...}

// Inside a regular function, `this` depends on how it's called
function logThis() {
  console.log(this);
}
logThis(); // Window (or undefined in strict mode)
logThis.call("hello"); // "hello" — .call() sets `this` explicitly

// Arrow functions do NOT have their own `this`
// They inherit `this` from the surrounding scope
const object3 = {
  method: () => {
    console.log(this); // Window — NOT the object!
  },
};

// Regular method has its own `this`
const object4 = {
  method() {
    console.log(this); // { method: f } — the object itself
  },
};
```

### Built-in classes

JS has built-in classes you use every day:

```js
// Date
const date = new Date();
console.log(date);
console.log(date.toLocaleTimeString()); // e.g. "3:45:12 PM"

// Other common built-in classes: Array, Map, Set, Promise, Error
```

---

## Lesson 19 — Backend, Callbacks, Promises & Async/Await

**Files:** `lesson-18/scripts/checkout.js`, `lesson-18/data/products.js`, `lesson-18/scripts/checkout/paymentSummary.js`

### HTTP & the network

- **HTTP** is the protocol browsers use to talk to servers.
- **GET** — fetch data from a server.
- **POST** — send data to a server.
- **URL paths** — `https://supersimplebackend.dev/products` — the `/products` part is the path.
- **Status codes** — `200 OK`, `404 Not Found`, `500 Server Error`.

### XHR + Callback (old approach)

The callback is passed as a function argument and called when the async work finishes:

```js
// products.js
export function loadProducts(callback) {
  const xhr = new XMLHttpRequest();

  xhr.addEventListener("load", () => {
    products = JSON.parse(xhr.response).map((details) => {
      if (details.type === "clothing") return new Clothing(details);
      return new Product(details);
    });
    callback(); // notify the caller that loading is done
  });

  xhr.addEventListener("error", () => {
    console.log("Unexpected error. Please try again later.");
  });

  xhr.open("GET", "https://supersimplebackend.dev/products");
  xhr.send();
}

// amazon.js — caller passes what to do next as a callback
loadProducts(renderProductsGrid);
```

**Problem with callbacks:** nesting multiple callbacks creates hard-to-read "callback hell":

```js
loadProducts(() => {
  // wait for products
  loadCart(() => {
    // then wait for cart
    renderOrderSummary(); // deeply nested
    renderPaymentSummary();
  });
});
```

### Promises

A **Promise** is an object that represents a future value. It's either pending, resolved (success), or rejected (error).

```js
// Creating a promise manually
const promise = new Promise((resolve, reject) => {
  // do async work...
  resolve("value1"); // success — passes a value to .then()
  // reject('error1');  // failure — passes a value to .catch()
});

// Consuming with .then() and .catch()
promise
  .then((value) => {
    console.log(value); // "value1"
    return "next value";
  })
  .then((value) => {
    console.log(value); // "next value" — chains are flat, not nested
  })
  .catch((error) => {
    console.log(error); // handles any rejection in the chain
  });
```

### Wrapping a callback-based function in a Promise

```js
new Promise((resolve) => {
  loadProducts(() => {
    resolve("value1");
  });
})
  .then(() => {
    return new Promise((resolve) => {
      loadCart(() => {
        resolve();
      });
    });
  })
  .then(() => {
    renderOrderSummary();
    renderPaymentSummary();
  });
```

### Promise.all — run multiple promises in parallel

```js
Promise.all([
  loadProductsFetch(),
  new Promise((resolve) => {
    loadCart(() => {
      resolve();
    });
  }),
]).then((values) => {
  console.log(values); // array of resolved values
  renderOrderSummary();
  renderPaymentSummary();
});
```

Both promises start at the same time. `.then()` runs only after **both** finish.

### fetch() — the modern way to make HTTP requests

`fetch()` returns a Promise automatically:

```js
// GET request
export function loadProductsFetch() {
  const promise = fetch("https://supersimplebackend.dev/products")
    .then((response) => {
      return response.json(); // parse JSON — also returns a Promise
    })
    .then((productsData) => {
      products = productsData.map((details) => {
        if (details.type === "clothing") return new Clothing(details);
        return new Product(details);
      });
    })
    .catch((error) => {
      console.log("Unexpected error. Please try again later.");
    });

  return promise;
}
```

**Key points:**

- `fetch()` returns a Promise that resolves to a `Response` object.
- `response.json()` parses the body as JSON — it also returns a Promise.
- You need **two** `.then()` calls: one to get the response, one to use the parsed data.

### async / await — cleaner syntax for Promises

`async`/`await` lets you write async code that looks synchronous. It's just syntax sugar over Promises.

```js
async function loadPage() {
  await loadProductsFetch(); // pause here until the promise resolves

  // continues once products are loaded
  renderOrderSummary();
  renderPaymentSummary();
}
loadPage();
```

- `async` before a function makes it return a Promise automatically.
- `await` pauses execution inside the function until the Promise resolves.
- Code after `await` runs only after the awaited operation finishes.

### Combining await with a wrapped callback

```js
async function loadPage() {
  await loadProductsFetch();

  // Wrap callback-style loadCart in a Promise so we can await it
  await new Promise((resolve, reject) => {
    loadCart(() => {
      resolve("value3");
    });
  });

  renderOrderSummary();
  renderPaymentSummary();
}
```

### Error handling

**In callbacks** — errors must be handled manually at each level:

```js
xhr.addEventListener("error", (error) => {
  console.log("Something went wrong.");
});
```

**In Promises** — `.catch()` at the end of a chain handles any rejection:

```js
fetch(url)
  .then(res => res.json())
  .then(data => { ... })
  .catch(error => {
    console.log('Error:', error);
  });
```

**In async/await** — use `try`/`catch`:

```js
async function loadPage() {
  try {
    await loadProductsFetch();

    await new Promise((resolve, reject) => {
      loadCart(() => {
        resolve();
      });
    });
  } catch (error) {
    console.log("Unexpected error. Please try again later.");
  }

  renderOrderSummary();
  renderPaymentSummary();
}
```

The `catch` block runs if **any** `await` in the `try` block rejects.

### Creating and throwing errors manually

```js
throw new Error("Something went wrong");
throw "error1"; // can throw any value, but Error objects are preferred
```

### POST request with fetch

Send data **to** the server (e.g. placing an order):

```js
document
  .querySelector(".js-place-order")
  .addEventListener("click", async () => {
    try {
      const response = await fetch("https://supersimplebackend.dev/orders", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          cart: cart,
        }),
      });

      const order = await response.json(); // parse the server's response
      addOrder(order);
    } catch (error) {
      console.log("Unexpected error. Try again later.");
    }

    window.location.href = "orders.html"; // redirect to next page
  });
```

### URL parameters

URL parameters pass data between pages via the URL string:

```
orders.html?orderId=abc123&trackingId=xyz
```

```js
// Reading parameters from the current page URL
const params = new URLSearchParams(window.location.search);
const orderId = params.get("orderId"); // "abc123"
const trackingId = params.get("trackingId"); // "xyz"
```

### Asynchronous code — the mental model

```
Synchronous:   line 1 → line 2 → line 3  (each waits for the one before)
Asynchronous:  line 1 starts, line 2 runs immediately, line 1 finishes later
```

```js
setTimeout(() => {
  console.log("timeout"); // runs after 3 seconds
}, 3000);

console.log("next line"); // runs immediately — doesn't wait for timeout
```

`async`/`await` gives you the **readability** of synchronous code while keeping the **non-blocking** behaviour of async code.

---

## Quick Reference

### Comparison operators

| Operator | Meaning                     |
| -------- | --------------------------- |
| `===`    | Strict equal (type + value) |
| `!==`    | Strict not equal            |
| `>`      | Greater than                |
| `>=`     | Greater than or equal       |
| `<`      | Less than                   |
| `<=`     | Less than or equal          |

### Common array methods

| Method             | What it does                               |
| ------------------ | ------------------------------------------ |
| `push(item)`       | Add item to end                            |
| `splice(i, n)`     | Remove n items starting at index i         |
| `slice()`          | Shallow copy                               |
| `forEach(fn)`      | Run fn for each item                       |
| `filter(fn)`       | New array with items where fn returns true |
| `map(fn)`          | New array with each item transformed by fn |
| `Array.isArray(x)` | Check if x is an array                     |

### Common string methods

| Method           | What it does                     |
| ---------------- | -------------------------------- |
| `.length`        | Number of characters             |
| `.toUpperCase()` | All caps                         |
| `.toLowerCase()` | All lowercase                    |
| `.includes(str)` | Returns true if contains str     |
| `.trim()`        | Remove whitespace from both ends |

### DOM quick reference

```js
document.querySelector(".class"); // first match
document.querySelectorAll(".class"); // NodeList of all matches
element.innerHTML = "<b>html</b>"; // set inner HTML
element.innerText; // get/set visible text
element.classList.add("name"); // add CSS class
element.classList.remove("name"); // remove CSS class
element.dataset.someKey; // read data-some-key attribute
element.addEventListener("click", fn); // attach event listener
element.removeEventListener("click", fn); // detach event listener
element.remove(); // remove element from DOM
```
