<div id="top"></div>

# 📘 HTML & CSS Notes

---

<details>
<summary>Table of contents</summary>

- [CSS Fundamentals](#-1-css-fundamentals)
- [Layout Systems](#-2-layout-systems)
- [Selectors](#-3-selectors)
- [Specificity](#️-4-specificity)
- [Inheritance](#-5-inheritance)
- [Visual Styling](#-6-visual-styling)
- [Sizing & Units](#-7-sizing--units)
- [Float & Visibility](#-8-float--visibility)
- [Fonts](#-9-fonts)
- [Text Styling](#️-10-text-styling)
- [Transforms & Animations](#️-11-transforms--animations)
- [Advanced CSS](#-12-advanced-css)
- [Utility Tricks](#-13-utility-tricks)
- [Accessibility](#-14-accessibility)
- [Pseudo Content](#-15-pseudo-content)
- [Scrollable List](#-16-scrollable-list-example)
- [Misc](#-17-misc)
- [Resources]
- [Summary](#-summary)

</details>


## 📦 1. CSS Fundamentals

### Box Model
content → padding → border → margin

### Display
- Block → div, p
- Inline → span, strong, u
- Inline-block → img, input

### Position
- static, relative, absolute, fixed
- top, left, right, bottom, z-index

---

## 🧱 2. Layout Systems

### Flexbox (1D)
- justify-content
- align-items
- align-content
- flex: grow shrink basis
- flex-wrap
- align-self

### Grid (2D)
- align-items, justify-items
- place-items
- justify-content, align-content
- grid-template

---

## 🎯 3. Selectors

### Basic
- type → p, div
- id → #id
- class → .class
- attribute → a[href], a[target="_blank"]

### Relational
- parent child → #id p
- direct child → #id > p
- next sibling → #id + p
- general sibling → #id ~ p

### Pseudo-class
:first-child, :last-child, :nth-child(), :hover, :focus

### Pseudo-element
::before, ::after, ::first-letter, ::first-line

<p align="right">(<a href="#top">back to top</a>)</p>
---

## ⚖️ 4. Specificity
!important > id > class > element

---

## 🔁 5. Inheritance
- color: initial
- border: inherit

---

## 🎨 6. Visual Styling

### Gradients
- linear-gradient()
- radial-gradient()

### Shadows
- box-shadow
- text-shadow

---

## 📏 7. Sizing & Units

### Box Sizing
box-sizing: border-box

### Units
- px
- %
- vw, vh
- em, rem

---

## 🌊 8. Float & Visibility

### Float
- float: left
- clear: both

### Visibility
- display: none
- visibility: hidden

<p align="right">(<a href="#top">back to top</a>)</p>
---

## 🔤 9. Fonts

### Sources
- fonts.google.com
- fontsquirrel.com

### Font Display
- swap, block, fallback, optional

---

## ✍️ 10. Text Styling

### Spacing
- line-height
- letter-spacing
- word-spacing

### Formatting
- text-align
- text-transform
- text-indent
- white-space
- text-overflow

### Columns
- column-count
- column-gap
- column-rule

---

## 🎞️ 11. Transforms & Animations

### Transform
- perspective
- rotateY

### Animation
- animation-name
- duration
- timing-function

---

## ✨ 12. Advanced CSS

### Glass Effect
backdrop-filter: blur()

### Overflow
overflow: hidden | scroll | auto

### Aspect Ratio
aspect-ratio

### Filters
filter: blur()

### Object Fit
object-fit: cover

<p align="right">(<a href="#top">back to top</a>)</p>
---

## 🧠 13. Utility Tricks

- scroll-behavior: smooth
- pointer-events: none
- list-style: none

---

## ♿ 14. Accessibility

### Screen Reader Only
.sr-only { position: absolute; width: 1px; height: 1px; overflow: hidden; }

---

## 🧩 15. Pseudo Content

p::before { content: "Question - "; }

---

## 📜 16. Scrollable List Example

nav ul {
  list-style: none;
  height: 270px;
  overflow-y: auto;
  overflow-x: hidden;
}

---

## 📌 17. Misc

- Colors → rgba, hsla, hex
- Elements → span, strong, u
- role attribute

---

## Resources

- **images**
    - Webp - https://giphy.com/
    - unplash - https://unsplash.com/

- **fonts**
  - google fonts
  - [font face]1001 fonts - https://www.1001fonts.com/

- **colors**
  - fetch colors from image - https://coolors.co/

- **web - accessibility**
  - to check contrast of colors - https://webaim.org/resources/contrastchecker/

## 🚀 Summary

- Flexbox → 1D layout
- Grid → 2D layout
- Selectors → targeting
- Position → placement
- Units → responsiveness

<p align="right">(<a href="#top">back to top</a>)</p>