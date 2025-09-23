# JavaScript Basics – Quick Reference

## HTML / CSS / JS Roles
- **HTML** – Create the content  
- **CSS** – Change the appearance  
- **JavaScript** – Makes it interactive  

### Main Idea of JavaScript
- Save data  
- Generate HTML  
- Make it interactive  

---

## JavaScript Core Concepts

### Floating-Point Issue  
`0.1 + 0.2 // ≈ 0.30000000000000004`

### Console  
```js
alert('Hello');
2 + 2;
document.body.innerHTML = 'Hello';
console.log('Hi');
```
Use **console.log()** to print results.  
Use `<script>` in HTML or link external JS with `<script src="file.js"></script>`.

---

## Type System

### Type Coercion (Implicit Conversion)
```js
console.log('25' - 5); // 20
console.log('25' * 5); // 125
console.log('25' / 5); // 5
```

### Type Conversion (Explicit)
```js
Number('123');
String(123);
typeof 123; // 'number'
```

---

## Strings
- `'...'` or `"..."` or `` `...` `` (Template Strings)
- Template Strings support:
  - Interpolation: `` `Temp: ${10+1}` ``
  - Multi-line strings

---

## Variables
- **Rules:**  
  - No reserved keywords  
  - Not starting with numbers  
  - Only `$` or `_` as special chars  

- **let** – Block scope, updatable  
- **const** – Block scope, not updatable  
- **var** – Function/global scope  

**Naming Conventions:** camelCase (preferred), PascalCase, kebab-case (CSS), snake_case.

---

## Booleans & Comparisons
- `true` / `false`  
- Operators: `> < >= <= === !==`  
- `==` allows coercion, `===` strict comparison  

---

## Order of Operations
`(), *, /, +, -, comparisons, logical operators`  

**Accumulators:** `+=, -=`  
**.toFixed()** fixes decimal places.

---

## Data Attributes
```html
<button data-product-name="basketball">Add to cart</button>
```
```js
button.dataset; 
button.dataset.productName;
```

---

## Truthy & Falsy
- **Falsy:** false, 0, NaN, undefined, null  
- **Truthy:** Everything else  

Shortcuts:
- **Ternary:** `condition ? a : b`
- **Guard:** `condition && doSomething()`
- **Default:** `value || defaultValue`

---

## Functions
```js
function greet(name = 'User') {
  console.log(`Hi ${name}`);
}
greet('Hemanth');
```
- Parameters receive values  
- Arguments send values  

---

## Objects
```js
const product = {
  name: 'Shirt',
  price: 1100,
  'delivery-time': '1 day',
  rating: { stars: 4.5, count: 87 },
  fun() { console.log('method inside object'); }
};

console.log(product.name);
console.log(product['delivery-time']);
console.log(product.rating.stars);
product.fun();
```
- Objects compare by reference  
- Destructuring:  
```js
const { name, price } = product;
```

---

## Built-in Objects

### Math
```js
Math.random();
Math.round();
Math.floor();
Math.ceil();
```

### Local Storage
```js
localStorage.setItem('key', value);
localStorage.getItem('key');
localStorage.removeItem('key');
```

### JSON
- Stringify JS object → JSON: `JSON.stringify(obj)`
- Parse JSON → JS object: `JSON.parse(jsonStr)`
- JSON supports only data, not functions  

### DOM  
```js
document.querySelector('button');
document.querySelectorAll('.class');
document.querySelector('.input').value;
document.querySelector('.input').remove();

document.querySelector('.input')
  .addEventListener('click', () => { ... });
```

**classList:**  
`.add()`, `.remove()`, `.contains()`, `.toggle()`

---

## Events  
Common events:  
- click, keydown, scroll, mouseenter, mouseleave  

Every event listener gets an **event object**:  
`event.key`

---

## Window  
Browser object model:  
```js
window.document;
window.console.log('Hi');
window.addEventListener('scroll', () => {...});
```

---

## Arrays
```js
const arr = [1, 'hello', {name:'socks'}];
Array.isArray(arr);
arr.push(4);
arr.pop();
arr.splice(1, 1);
arr.forEach((val, i) => {});
arr.filter(val => val > 2);
arr.map(val => val * 2);
```

Destructuring:  
`const [a, b] = [1, 2, 3];`

---

## Loops
- `while()`, `for()`  
- `forEach()` for arrays (no `break`/`continue`)  

---

## Functions – Advanced
- Hoisting allows calling function declarations before they appear  
- Function expressions and arrow functions are not hoisted  

Arrow functions:
```js
const fun = param => console.log(param);
const add = () => 10 + 1;
```

---

## Asynchronous Code
- **Synchronous:** waits  
- **Asynchronous:** doesn’t wait  

```js
setTimeout(() => console.log('Later'), 1000);
const id = setInterval(() => console.log('Repeating'), 2000);
clearInterval(id);
```

---

## Auto-Boxing
Strings, numbers, and booleans get wrapped in objects automatically:  
```js
'hello'.length;
'hello'.toUpperCase();
(3.1).toString();
true.toString();
```
