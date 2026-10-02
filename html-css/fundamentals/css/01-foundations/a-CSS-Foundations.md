# **1. CSS Foundations 🍐**

CSS stands for **Cascading Style Sheets**. It is a stylesheet language used to define the visual presentation of HTML documents controlling how elements appear on a webpage, including their colors, fonts, spacing, sizes, positioning, and overall layout.

---

## **a) What is CSS?**

CSS allows developers to transform plain HTML into visually appealing and organized webpages.

While HTML describes **what the content is**, CSS describes **how that content should look**.

For example, HTML can define a heading:

```html
<h1>Hello, world!</h1>
```

By default, the browser decides how that heading looks. With CSS, we can customize its appearance:

```css
h1 {
  color: darkgreen;
  font-size: 2.5rem;
  text-align: center;
}
```

CSS can control many aspects of a webpage, such as:

- Colors
- Typography
- Spacing
- Borders
- Backgrounds
- Element sizes
- Positioning
- Page layouts
- Responsive design
- Animations and transitions

This separation between **content** and **presentation** makes websites easier to design, maintain, and scale.

---

## **b) How CSS Connects to HTML**

Modern websites are generally built using three fundamental technologies:

- **HTML** — structure
- **CSS** — presentation
- **JavaScript** — behavior and interactivity

A simple way to understand their relationship is to compare a webpage to a human body.

### **HTML: The Structure**

HTML stands for **HyperText Markup Language**. It defines the structure and meaning of the content on a webpage.

For example:

```html
<h1>My Website</h1>

<p>Welcome to my website!</p>

<button>Click me</button>
```

HTML tells the browser that there is a heading, a paragraph, and a button.

In the human-body analogy, HTML would be the **skeleton and body structure**.

---

### **CSS: The Presentation**

CSS defines how the HTML elements should look.

For example:

```css
h1 {
  color: navy;
  font-family: Arial, sans-serif;
}

button {
  background-color: black;
  color: white;
  padding: 10px 20px;
}
```

CSS can be compared to the **clothes, hairstyle, colors, and visual appearance** of the body.

It does not change what the HTML elements are; it changes how they are presented.

---

### **JavaScript: The Behavior**

JavaScript is a programming language commonly used to add logic and interactivity to webpages.

For example, JavaScript can make a button respond when a user clicks it:

```html
<button id="helloButton">Click me</button>

<script>
  const button = document.querySelector("#helloButton");

  button.addEventListener("click", function () {
    alert("Hello!");
  });
</script>
```

Following the same analogy, JavaScript can be thought of as the **behavior and actions** of the body.

A simplified way to remember the three technologies is:

```text
HTML       → Structure
CSS        → Presentation
JavaScript → Behavior
```

---

## **c) Inline, Internal, and External CSS**

CSS can be added to an HTML document in three main ways:

1. Inline CSS
2. Internal CSS
3. External CSS

---

### **Inline CSS**

Inline CSS is written directly inside an HTML element using the `style` attribute.

```html
<h1 style="color: red;">Hello, world!</h1>
```

In this example, the CSS declaration:

```css
color: red;
```

is applied directly to the `<h1>` element.

Inline CSS is useful for very small or temporary changes, but it is generally avoided in larger projects because it mixes HTML structure with visual styling.

For example, this quickly becomes difficult to maintain:

```html
<h1 style="color: red; font-size: 40px; text-align: center;">My Website</h1>
```

---

### **Internal CSS**

Internal CSS is written inside a `<style>` element, which is usually placed inside the `<head>` section of an HTML document.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My Website</title>

    <style>
      h1 {
        color: purple;
        text-align: center;
      }

      p {
        font-size: 18px;
      }
    </style>
  </head>

  <body>
    <h1>Hello!</h1>
    <p>This page uses internal CSS.</p>
  </body>
</html>
```

Internal CSS is useful when the styles are only needed for a single webpage.

However, if a website contains several pages, repeating the same `<style>` block in every HTML file would become inefficient.

---

### **External CSS**

External CSS stores the styles in a separate `.css` file.

For example, a project could have the following structure:

```text
project/
│
├── index.html
└── styles.css
```

The HTML document connects to the CSS file using the `<link>` element inside the `<head>`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My Website</title>

    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <h1>Hello, world!</h1>
  </body>
</html>
```

The CSS file could contain:

```css
h1 {
  color: darkgreen;
  font-size: 2.5rem;
}
```

The `href` attribute tells the browser where the stylesheet is located:

```html
href="styles.css"
```

The `rel` attribute describes the relationship between the HTML document and the linked file:

```html
rel="stylesheet"
```

External CSS is the most common approach for larger projects because the same stylesheet can be reused across multiple HTML pages.

For example:

```html
<link rel="stylesheet" href="styles.css" />
```

could be included in:

```text
index.html
about.html
contact.html
projects.html
```

All of those pages could then share the same design system.

---

## **d) Basic CSS Syntax**

CSS is a **rule-based language**.

Meaninga CSS stylesheet consists of rules that tell the browser:

> Select these HTML elements and apply these styles to them.

A basic CSS rule looks like this:

```css
selector {
  property: value;
}
```

For example:

```css
h1 {
  color: red;
  font-size: 2.5rem;
}
```

This rule tells the browser to select every `<h1>` element and apply the specified styles.

Consider the following HTML:

```html
<h1>CSS Foundations</h1>
```

With this CSS:

```css
h1 {
  color: red;
  font-size: 2.5rem;
}
```

the heading will appear red and with a larger font size.

A CSS rule contains several important parts:

```css
h1 {
  color: red;
  font-size: 2.5rem;
}
```

Here:

```text
h1          → selector

color       → property
red         → value

font-size   → property
2.5rem      → value
```

The content between the curly braces `{ }` is called the **declaration block**.

---

## **e) Selectors**

A **selector** determines which HTML element or group of elements a CSS rule should target.

Consider the following rule:

```css
p {
  color: blue;
}
```

The selector is:

```css
p
```

This means that the rule will target every `<p>` element on the page.

For example:

```html
<p>First paragraph</p>
<p>Second paragraph</p>
```

Both paragraphs will receive the style:

```css
p {
  color: blue;
}
```

Selectors are extremely important because they determine **where CSS rules are applied**.

Some common selector types include element selectors, class selectors, and ID selectors.

### Element Selector

An element selector targets every HTML element of a specific type.

```css
h2 {
  color: green;
}
```

This targets every `<h2>` element.

---

### Class Selector

A class selector targets elements that contain a specific `class` attribute.

HTML:

```html
<p class="important">Important message</p>
<p>Normal message</p>
```

CSS:

```css
.important {
  font-weight: bold;
}
```

Class selectors begin with a period:

```css
.class-name {
}
```

Classes are useful because the same class can be reused across many elements.

```html
<p class="highlight">Paragraph</p>
<span class="highlight">Text</span>
<button class="highlight">Button</button>
```

```css
.highlight {
  background-color: yellow;
}
```

---

### ID Selector

An ID selector targets an element with a specific `id` attribute.

HTML:

```html
<h1 id="main-title">My Website</h1>
```

CSS:

```css
#main-title {
  color: darkblue;
}
```

ID selectors begin with a hash symbol:

```css
#id-name {
}
```

Unlike classes, an ID should generally identify one unique element within a page.

---

## **f) Declarations**

A **declaration** defines a specific style that should be applied to the selected element.

For example:

```css
p {
  color: blue;
}
```

The declaration is:

```css
color: blue;
```

A declaration contains two parts:

```text
property: value;
```

In this case:

```text
property → color
value    → blue
```

Multiple declarations can exist inside the same declaration block:

```css
p {
  color: blue;
  font-size: 18px;
  line-height: 1.5;
}
```

Each declaration should normally end with a semicolon `;`

Although the final declaration may sometimes work without one, consistently using semicolons makes the code clearer and prevents errors when additional declarations are added later.

---

## **g) Properties and Values**

CSS declarations consist of **properties** and **values**.

A property represents the characteristic that we want to modify.

A value specifies how that characteristic should appear.

For example:

```css
h1 {
  color: purple;
}
```

Here:

```text
color  → property
purple → value
```

Another example:

```css
p {
  font-size: 20px;
}
```

Here:

```text
font-size → property
20px      → value
```

Different CSS properties accept different types of values.

For example, colors can be written in several ways:

```css
color: red;
```

```css
color: #ff0000;
```

```css
color: rgb(255, 0, 0);
```

Sizes can also use different units:

```css
font-size: 16px;
```

```css
font-size: 1.2rem;
```

```css
width: 50%;
```

A single CSS rule can combine many different properties:

```css
.card {
  background-color: white;
  width: 300px;
  padding: 20px;
  border-radius: 12px;
  font-size: 1rem;
}
```

Understanding the relationship between **selectors, declarations, properties, and values** is one of the most important foundations of CSS.

A useful mental model is:

```text
CSS Rule
│
├── Selector
│
└── Declaration Block
    │
    ├── Property: Value;
    ├── Property: Value;
    └── Property: Value;
```

For example:

```css
button {
  background-color: black;
  color: white;
  padding: 10px;
}
```

can be understood as:

```text
button                    → Selector

background-color: black;  → Declaration
color: white;             → Declaration
padding: 10px;            → Declaration

background-color          → Property
black                     → Value
```

---

## **References**

- MDN Web Docs — CSS
- MDN Web Docs — Getting Started with CSS
- MDN Web Docs — CSS Selectors
- CSS Specifications — World Wide Web Consortium (W3C)
- Ansari, A. (s.f.). What the heck is HTML & CSS? Learning web development the right way. Medium. https://medium.com/@anasansari157/what-the-heck-is-html-css-28147821ee8a
- MDN contributors. (s.f.). What is CSS? MDN Web Docs. Mozilla. https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/What_is_CSS
- Umbraco. (s.f.). What is CSS and how is CSS used on websites? Umbraco Knowledge Base. https://umbraco.com/knowledge-base/css/
- Tutorials Point. (s.f.). CSS - Introduction. Tutorials Point. https://www.tutorialspoint.com/css/what_is_css.htm
