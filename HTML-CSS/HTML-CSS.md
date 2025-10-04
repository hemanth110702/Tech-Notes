

## HTML Basics

- <button>Hello</button> Creates a button with the text "Hello" inside.
- <p>paragraph of text</p> Creates a paragraph of text

## HTML Syntax

- Syntax = rules for writing HTML code (like grammar in English)
  - 1. Elements should have an opening tag and a matching closing tag.
  - <img width="382" height="170" alt="syntax" src="https://github.com/user-attachments/assets/e78dee05-3031-43f8-b329-44f470581329" />
  - 2. In HTML, extra spaces and newlines are combined into 1 space.
<p>paragraph of text</p>
<p>paragraph of text</p>
<p>
paragraph of text
</p>
All 3 examples above will show the same result on the web page.

## Attributes

Attributes modify how an HTML element behaves.
<a href="https://youtube.com" target="_blank">
Link to YouTube
</a>

<a> = link to another website.
href = modifies which website is opened when clicking this link.
target="_blank" causes the link
to be opened in a new tab.

## CSS Basics

One way of writing CSS code is using the <style> HTML element.

<style>
button {
background-color: red;
color: white;
}
</style>

Modifies all <button>s on the page.
Change background color to red.
Change text color to white.

## CSS Syntax

<img width="448" height="245" alt="css syntax" src="https://github.com/user-attachments/assets/af77b668-b17f-4ee8-b510-b49e35397872" />

## CSS Properties

Here are some common CSS properties we can use:
button {
background-color: red; Sets the background color. 
                    Common values:
                          ● Color name: red, white, black
                          ● rgb value: rgb(0, 150, 255);
                          ● Hex value: #0096FF
color: white; 
                    Sets the text color. Takes the same values as
                    background-color (color name, rgb, hex).
height: 36px; 
                    Sets the height. Common values:
                    ● Pixel value: 36px
                    ● Percentage: 50%
width: 105px; 
                    Sets the width. Takes the same values as height.
border: none; 
                    Removes the border.
border-radius: 2px; 
                    Creates rounded corners.
cursor: pointer; 
                    Changes the mouse/cursor when hovering over the element.
border-color: red; 
                    Sets the border color.
border-style: solid; 
                    Sets the border style. Common values:
                    ● solid
                    ● dotted
                    ● dashed
border-width: 1px; 
                    Sets the border width.
}

## How To Google CSS Properties
We regularly use Google to search for CSS properties that we don't know or don't remember.
When using Google, search what you're trying to accomplish. Exampes:
"css rounded corners"
"css text italic"
"css adjust space between lines"

## CSS Values

Each CSS property has a set of values that are allowed (background-color allows color values,
cursor allows solid, dotted, dashed, etc.)
Here are some categories of values that are useful to know:
Color Values
1. A color name: red, white, black
2. RGB value: rgb(0, 150, 255);
RGB is a more precise way of measuring color. Every color can be created using a
combination of red, green, and blue (RGB). In CSS, this is represented by rgb(...);

<img width="256" height="112" alt="color val" src="https://github.com/user-attachments/assets/abad2cca-0607-4189-afc4-63d54744f57f" />

3. Hex value
Hex is another way to write RGB.
<img width="190" height="95" alt="hex val" src="https://github.com/user-attachments/assets/be3bea48-0066-4595-84f3-c523a88772da" />


● Each character in Hex is base 16, which means it can have a value of 0, 1, 2, ... 8, 9, A, B, C,
D, E, F (16 possible values).
● Using the first 2 characters, we can have 16 * 16 = 256 possible values from 0 - 255:
00 = 0
01 = 1
...
0F = 15
10 = 16
11 = (1 * 16) + 1 = 17
...
FF = (15 * 16) + 15 = 255
● This is the same range as RGB (0 to 255), so the first 2 characters in Hex are used to
represent red, the second 2 characters represent green, and the third 2 characters
represent blue. Usually, it's easier to use a Hex to RGB calculator to convert.

4. RGBA value: rgba(0, 150, 255, 0.5);
Same as RGB, except with an additional a-value (alpha value). The a-value determines
how see-through the color is. 0 = complete see-through, 1 = solid color and not
see-through, 0.5 = 50% see-through.


Measurement Values
1. Pixels: 50px, 100px
Pixels (px) are a common unit of measurement in the digital world.
For example: a 4K screen is 3840px by 2160px.
2. Percent: 50%, 100%
A relative measurement. For example, width: 50%; means 50% of the width of the page
(or if the element is inside another element, 50% of the width of the container element).
3. em / rem: 1em, 1rem
Relative measurements that are useful for accessibility.
em = relative to the font-size of the element (2em means 2 times the font size).
rem = relative to the font-size of the page, which is 16px by default (2rem means 2 times
the font size of the page = 2 * 16px = 32px by default).

## Class Attribute
Class attribute = lets us target specific elements with CSS.

<button class="subscribe-button">
SUBSCRIBE
</button>

Add a class to an element. The class name (the
text between the "...") can be anything you
want, but no spaces

.subscribe-button {
...
}

Target all elements on the page with
class="subscribe-button"


<button class="youtube-button">
SUBSCRIBE
</button>
<button class="youtube-button">
JOIN
</button>

Multiple elements can have the same class


<button class="youtube-button subscribe-button">
SUBSCRIBE
</button>

An element can have multiple
classes, separated by space


button {
...
}
.youtube-button {
...
}
.subscribe-button {
...
}
Elements can be targeted by multiple CSS selectors.
Here, all 3 CSS selectors will target the button above.


## CSS Pseudo-Classes

.subscribe-button:hover {
...
}
These styles only apply when hovering over an
element with class="subscribe-button"

.subscribe-button:active {
...
}
These styles only apply when clicking on an element
with class="subscribe-button"

## Intermediate CSS Properties

.subscribe-button {
opacity: 0.5; Sets how see-through an element is: 0.5 = 50% see-through.
opacity: 0; 0 = complete see-through (invisible).
opacity: 1; 1 = not see-through (this is the default value).
transition: <property> <duration>; 
                      Transition smoothly when changing styles
                      (often used when hovering).
transition: background-color 1s; 
                      Transition background color over 1 second.
transition: color 0.15s;
                      Transition text color over 0.15 seconds.
transition: <property1> <duration1>,
<property2> <duration2>,
...;
                      Transition multiple properties by separating
                      them with a comma.
transition: background-color 0.15s,
color 0.15s;
                      Transition both background color and text
                      color over 0.15 seconds.
box-shadow: <h-position> <v-position> <blur> <color>;
box-shadow: 3px 4px 5px black; 
                      Creates a shadow that's 3px to the right of
                      the element, 4px to the bottom, with 5px of
                      blur, and color of black.
box-shadow: 3px 4px 0 rgba(0, 0, 0, 0.15);
                      Creates a shadow that's 3px to the
                      right, 4px to the bottom, with no blur,
                      and a very faint black color.
}

## Chrome DevTools
Lets us view (and modify) the HTML and CSS of a website directly in the browser.
To open the DevTools: right-click > Inspect.

<img width="593" height="365" alt="chrome dev tools" src="https://github.com/user-attachments/assets/c21ab891-0bd9-4af7-8107-3f07c2650a0e" />

## CSS Box Model
● Determines how much space an element takes up.
● Determines how far away elements are from each other

<img width="723" height="215" alt="CSS Box Model" src="https://github.com/user-attachments/assets/28dbaecc-06a2-4d8d-918c-597ff704f82f" />

.join-button {
margin-right: 10px; Add 10px of space on the outside of the element.
margin-left: 10px;
margin-top: 10px; Normal margin pushes things away from an element.
margin-bottom: 10px; margin-right: -20px; Negative margin pulls things towards an element like this:

<img width="210" height="66" alt="neg margin - towards" src="https://github.com/user-attachments/assets/a8d70d3e-73ab-4a5d-876a-e4cfb37d9c3a" />



margin: 10px; Shorthand for adding 10px of margin on all sides.
margin: 10px 20px; Add 10px of margin top & bottom and 20px left & right
margin: <top> <left & right> <bottom>;
margin: <top> <right> <bottom> <left>;

padding-right: 10px; Add 10px of space on the inside of the element.
padding-left: 10px;
padding-top: 10px;
padding-bottom: 10px;
padding-right: -20px; Negative padding has no effect.

padding: 10px; Shorthand for adding 10px of padding on all sides.
padding: 10px 20px; Add 10px of padding top & bottom and 20px left & right
padding: <top> <left & right> <bottom>;
padding: <top> <right> <bottom> <left>;

border-width: 1px; Sets the border width.
border-style: solid; Sets the border style (to a solid color).
border-color: red; Sets the border color.

border: <width> <style> <color>; Shorthand for the 3 properties above.
border: 1px solid red;
}

## Text Styles
.title {
font-family: Arial;
font-family: Roboto, Verdana, Arial;
                      Change the font.
                      A font-stack: if Roboto is not available, it will
                      fall back to Verdana. If Verdana is not
                      available it will fall back to Arial.
font-size: 30px; Change text size.
font-weight: bold; Change text thickness.
font-weight: 700;
                      Another way to specify font-weight. We can use: 100, 200,
                      300, ..., 900. bold = 700, regular = 400, semibold = 500
font-style: italic;
text-align: center; Other values we can use: left, right, justified
line-height: 24px; Adjust space between lines of text.
text-decoration: underline; Underlines the text.
text-decoration: none; Removes underline.
}

<p> by default have margin-top and margin-bottom. A common practice is to:
1. Reset the default margins.
p {
margin-top: 0;
margin-bottom: 0;
}
2. Then apply more precise margins.
.title {
margin-bottom: 16px;
}

Text Elements (also called Inline Elements)
● Text elements (<strong>, <u>, <span>, <a>) appear within a line of text.
<p>
This is a <strong>text element</strong>
</p>
Useful if we want to style only a part of the text.
● <span> is the most generic text element (it doesn't have any default styles).
● We can style text elements using a class:
<p>
This is a <span class="shop-link">text element</span>
</p>
.shop-link {
text-decoration: underline;
}