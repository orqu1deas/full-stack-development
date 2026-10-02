# **11. Flexbox 📦**

**Flexbox**, short for **Flexible Box Layout**, is a CSS layout model designed to make it easier to organize, align, and distribute elements inside a container.

Flexbox is especially useful when building interfaces that need to adapt to different screen sizes because it gives developers direct control over the direction, alignment, spacing, and size of elements.

Flexbox is considered a **one-dimensional layout system**. This means that it primarily handles layout in **one direction at a time**:

- Horizontally, as a **row**
- Vertically, as a **column**

Unlike CSS Grid, which is designed to work with rows and columns simultaneously, Flexbox focuses on arranging elements along a **main axis** and a **cross axis**.

A basic Flexbox layout can be created with:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex;
}
```

Once `display: flex` is applied, the direct children of `.container` become **flex items**.

---

## **a) Flex Containers**

A **flex container** is an element whose layout is controlled using Flexbox.

To create one, the `display` property is set to either:

```css
display: flex;
```

or:

```css
display: inline-flex;
```

For example:

```html
<div class="container">
  <div>Apple</div>
  <div>Pear</div>
  <div>Orange</div>
</div>
```

```css
.container {
  display: flex;
}
```

The `.container` element becomes the **flex container**, while its direct children become **flex items**.

### **`flex` vs. `inline-flex`**

With:

```css
.container {
  display: flex;
}
```

the flex container behaves like a block-level element and normally occupies the available width.

With:

```css
.container {
  display: inline-flex;
}
```

the container behaves more like an inline-level element and generally takes only the space required by its content.

The internal Flexbox behavior is otherwise similar.

---

### **Default Flexbox Behavior**

When a flex container is created with:

```css
.container {
  display: flex;
}
```

the browser applies several default values.

Conceptually, it behaves approximately like this:

```css
.container {
  display: flex;

  flex-direction: row;
  flex-wrap: nowrap;

  justify-content: flex-start;
  align-items: stretch;
}
```

Flex items also have default flexibility:

```css
.item {
  flex-grow: 0;
  flex-shrink: 1;
  flex-basis: auto;
}
```

As a result:

- Items are arranged horizontally.
- Items begin at the start of the main axis.
- Items do not grow automatically.
- Items are allowed to shrink when necessary.
- Items remain on a single line by default.
- Items stretch along the cross axis when their size is `auto`.

For example:

```html
<div class="container">
  <div class="item">One</div>
  <div class="item">Two</div>
  <div class="item">Three</div>
</div>
```

```css
.container {
  display: flex;
  border: 2px solid black;
}

.item {
  padding: 20px;
  border: 1px solid gray;
}
```

The three elements will appear next to each other in a horizontal row.

---

## **b) Flex Items**

A **flex item** is any **direct child** of a flex container.

Consider:

```html
<div class="container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```

```css
.container {
  display: flex;
}
```

The three `.item` elements are flex items because they are direct children of `.container`.

However, elements nested inside a flex item do **not automatically become flex items**.

For example:

```html
<div class="container">
  <div class="item">
    <span>Nested element</span>
  </div>
</div>
```

Here:

```text
.container → Flex container
.item      → Flex item
span       → Normal nested element
```

If we wanted `.item` to control its own children using Flexbox, we could also make it a flex container:

```css
.item {
  display: flex;
}
```

An element can therefore be both:

- A **flex item** relative to its parent
- A **flex container** for its own children

This pattern is extremely common in real-world layouts.

---

## **c) Main Axis and Cross Axis**

Flexbox organizes elements according to two conceptual axes:

- **Main axis**
- **Cross axis**

Understanding these two axes is essential because many Flexbox properties work relative to them rather than directly referring to horizontal or vertical positioning.

---

### **Main Axis**

The **main axis** is the primary direction in which flex items are arranged.

Its direction is determined by the `flex-direction` property.

For example:

```css
.container {
  display: flex;
  flex-direction: row;
}
```

With `row`, the main axis generally runs horizontally:

```text
Main axis →

[ Item 1 ] [ Item 2 ] [ Item 3 ]
```

If instead we write:

```css
.container {
  display: flex;
  flex-direction: column;
}
```

the main axis becomes vertical:

```text
Main axis ↓

[ Item 1 ]

[ Item 2 ]

[ Item 3 ]
```

Therefore, the main axis is **not always horizontal**.

It depends on `flex-direction`.

---

### **Cross Axis**

The **cross axis** runs perpendicular to the main axis.

If:

```css
flex-direction: row;
```

then:

```text
Main axis  → Horizontal
Cross axis ↓ Vertical
```

If:

```css
flex-direction: column;
```

then:

```text
Main axis  ↓ Vertical
Cross axis → Horizontal
```

This distinction becomes important when working with alignment properties.

In general:

```text
justify-content → Main axis
align-items     → Cross axis
```

For example:

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

The items are centered along both axes.

---

## **d) Flexbox Properties**

Flexbox properties can generally be divided into two groups:

### **Properties applied to the flex container**

```text
flex-direction
flex-wrap
flex-flow
justify-content
align-items
align-content
gap
```

### **Properties applied to flex items**

```text
flex-grow
flex-shrink
flex-basis
flex
align-self
order
```

It is important to know **where each property belongs**.

For example:

```css
.container {
  display: flex;
  justify-content: center;
}
```

is valid because `justify-content` applies to the **flex container**.

Meanwhile:

```css
.item {
  flex-grow: 1;
}
```

applies to the **flex item**.

---

# **Container Properties**

## **1. `flex-direction`**

The `flex-direction` property determines the direction of the **main axis** and therefore controls how flex items are arranged.

Its default value is:

```css
flex-direction: row;
```

There are four possible values:

```css
.container {
  flex-direction: row;
}
```

Items are arranged in a row.

```text
1 → 2 → 3
```

---

### **`row`**

```css
.container {
  display: flex;
  flex-direction: row;
}
```

```text
[1] [2] [3]
→
```

This is the default behavior.

---

### **`row-reverse`**

```css
.container {
  display: flex;
  flex-direction: row-reverse;
}
```

The items are arranged in the opposite direction.

```text
[3] [2] [1]
←
```

The visual order changes, but the order of the elements in the HTML document remains unchanged.

---

### **`column`**

```css
.container {
  display: flex;
  flex-direction: column;
}
```

Items are arranged vertically.

```text
[1]
 ↓
[2]
 ↓
[3]
```

---

### **`column-reverse`**

```css
.container {
  display: flex;
  flex-direction: column-reverse;
}
```

Items are arranged vertically in the opposite direction.

---

## **2. `justify-content`**

`justify-content` controls how flex items are distributed along the **main axis**.

Consider:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex;
  width: 800px;
}
```

If the items do not occupy all available space, `justify-content` determines where the remaining space goes.

---

### **`flex-start`**

```css
.container {
  justify-content: flex-start;
}
```

Items are grouped at the beginning of the main axis.

```text
[1][2][3]................
```

---

### **`flex-end`**

```css
.container {
  justify-content: flex-end;
}
```

Items are moved toward the end of the main axis.

```text
................[1][2][3]
```

---

### **`center`**

```css
.container {
  justify-content: center;
}
```

Items are centered.

```text
........[1][2][3]........
```

---

### **`space-between`**

```css
.container {
  justify-content: space-between;
}
```

The first and last items touch opposite edges, while the remaining space is distributed between the items.

```text
[1]..........[2]..........[3]
```

---

### **`space-around`**

```css
.container {
  justify-content: space-around;
}
```

Each item receives space around itself.

```text
..[1]....[2]....[3]..
```

The outer space is usually smaller than the space between items.

---

### **`space-evenly`**

```css
.container {
  justify-content: space-evenly;
}
```

All spaces are distributed equally.

```text
....[1]....[2]....[3]....
```

---

## **3. `align-items`**

`align-items` controls the alignment of flex items along the **cross axis**.

For example:

```css
.container {
  display: flex;
  height: 300px;

  align-items: center;
}
```

If `flex-direction` is `row`, this usually means vertical alignment.

Common values include:

```css
align-items: stretch;
align-items: flex-start;
align-items: flex-end;
align-items: center;
align-items: baseline;
```

---

### **`stretch`**

```css
.container {
  align-items: stretch;
}
```

This is the default value.

Items whose cross-axis size is `auto` stretch to fill the available space.

---

### **`flex-start`**

```css
.container {
  align-items: flex-start;
}
```

Items are aligned at the start of the cross axis.

---

### **`flex-end`**

```css
.container {
  align-items: flex-end;
}
```

Items are aligned at the end of the cross axis.

---

### **`center`**

```css
.container {
  align-items: center;
}
```

Items are centered along the cross axis.

---

### **`baseline`**

```css
.container {
  align-items: baseline;
}
```

Items are aligned according to their text baselines.

This can be useful when elements contain text with different font sizes.

---

## **4. Centering an Element with Flexbox**

One of the most common uses of Flexbox is centering content both horizontally and vertically.

HTML:

```html
<div class="container">
  <div class="card">Hello!</div>
</div>
```

CSS:

```css
.container {
  display: flex;

  justify-content: center;
  align-items: center;

  height: 100vh;
}
```

Because:

```text
justify-content → centers along the main axis
align-items     → centers along the cross axis
```

the `.card` becomes centered inside the viewport.

---

## **5. `flex-wrap`**

By default, flex items try to remain on a single line.

The default is:

```css
flex-wrap: nowrap;
```

If there is not enough space, the items may shrink rather than move to another line.

For example:

```css
.container {
  display: flex;
  flex-wrap: nowrap;
}
```

To allow items to move onto additional lines:

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
```

Possible values include:

```css
flex-wrap: nowrap;
flex-wrap: wrap;
flex-wrap: wrap-reverse;
```

---

### **Example**

```html
<div class="container">
  <div class="card">1</div>
  <div class="card">2</div>
  <div class="card">3</div>
  <div class="card">4</div>
  <div class="card">5</div>
</div>
```

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  width: 250px;
}
```

If the browser window becomes too narrow to display every card on one line, the cards can move to a new row.

This makes `flex-wrap` particularly useful for responsive layouts.

---

## **6. `flex-flow`**

`flex-flow` is a shorthand property that combines:

```text
flex-direction
+
flex-wrap
```

Instead of writing:

```css
.container {
  flex-direction: row;
  flex-wrap: wrap;
}
```

we can write:

```css
.container {
  flex-flow: row wrap;
}
```

---

## **7. `gap`**

The `gap` property defines spacing between flex items.

For example:

```css
.container {
  display: flex;
  gap: 20px;
}
```

Instead of manually adding margins to each item:

```css
.item {
  margin-right: 20px;
}
```

we can let the container control the spacing:

```css
.container {
  gap: 20px;
}
```

This is generally cleaner and easier to maintain.

For wrapped layouts, different row and column gaps can also be defined:

```css
.container {
  display: flex;
  flex-wrap: wrap;

  row-gap: 20px;
  column-gap: 40px;
}
```

Or using the shorthand:

```css
.container {
  gap: 20px 40px;
}
```

The first value represents the row gap, while the second represents the column gap.

---

## **8. `align-content`**

`align-content` controls the distribution of **multiple flex lines** along the cross axis.

This property is only meaningful when there are multiple lines.

For example:

```css
.container {
  display: flex;
  flex-wrap: wrap;

  height: 500px;

  align-content: center;
}
```

Common values include:

```css
align-content: flex-start;
align-content: flex-end;
align-content: center;
align-content: space-between;
align-content: space-around;
align-content: space-evenly;
align-content: stretch;
```

A common source of confusion is the difference between `align-items` and `align-content`.

```text
align-items
→ Aligns individual flex items inside a flex line.

align-content
→ Distributes multiple flex lines inside the container.
```

If the Flexbox layout has only one line, `align-content` usually has no visible effect.

---

# **Flex Item Properties**

## **9. `flex-grow`**

The `flex-grow` property determines whether a flex item can grow to occupy available space.

By default:

```css
.item {
  flex-grow: 0;
}
```

This means that items do not automatically grow.

Suppose we have:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item special">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex;
}

.item {
  width: 100px;
}

.special {
  flex-grow: 1;
}
```

The `.special` item will grow to consume the remaining available space.

---

### **Growth Ratios**

`flex-grow` can also determine how available space is distributed.

```css
.first {
  flex-grow: 1;
}

.second {
  flex-grow: 2;
}
```

The second item receives approximately twice as much of the **available free space** as the first.

It is important to understand that `flex-grow` distributes **remaining space**, not necessarily the item's total width.

---

## **10. `flex-shrink`**

The `flex-shrink` property determines how flex items shrink when there is not enough available space.

The default is:

```css
flex-shrink: 1;
```

This means flex items are allowed to shrink.

To prevent a specific item from shrinking:

```css
.item {
  flex-shrink: 0;
}
```

Example:

```css
.sidebar {
  width: 250px;
  flex-shrink: 0;
}
```

This can be useful when a sidebar should maintain a fixed width even when the available space becomes smaller.

---

## **11. `flex-basis`**

`flex-basis` defines the initial main-axis size of a flex item before the remaining space is distributed.

For example:

```css
.item {
  flex-basis: 200px;
}
```

When `flex-direction` is:

```css
flex-direction: row;
```

`flex-basis` usually acts similarly to an initial width.

When:

```css
flex-direction: column;
```

it behaves more like an initial height.

The default is:

```css
flex-basis: auto;
```

---

## **12. The `flex` Shorthand**

Instead of writing:

```css
.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 200px;
}
```

we can use:

```css
.item {
  flex: 1 1 200px;
}
```

The order is:

```text
flex: flex-grow flex-shrink flex-basis;
```

For example:

```css
.item {
  flex: 2 1 300px;
}
```

means approximately:

```css
.item {
  flex-grow: 2;
  flex-shrink: 1;
  flex-basis: 300px;
}
```

A very common pattern is:

```css
.item {
  flex: 1;
}
```

This tells the flex items to share the available space flexibly.

For example:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex;
}

.item {
  flex: 1;
}
```

The three items will generally share the available width equally.

---

## **13. `align-self`**

`align-self` allows one individual flex item to override the alignment defined by the container's `align-items`.

For example:

```css
.container {
  display: flex;
  align-items: center;
}
```

All items are centered along the cross axis.

However:

```css
.special {
  align-self: flex-end;
}
```

moves only the `.special` item toward the end of the cross axis.

Example:

```html
<div class="container">
  <div>1</div>
  <div class="special">2</div>
  <div>3</div>
</div>
```

```css
.container {
  display: flex;
  align-items: center;
  height: 300px;
}

.special {
  align-self: flex-end;
}
```

---

## **14. `order`**

By default, flex items appear according to their order in the HTML document.

For example:

```html
<div class="container">
  <div class="one">1</div>
  <div class="two">2</div>
  <div class="three">3</div>
</div>
```

Their default order is:

```text
1 → 2 → 3
```

The `order` property can visually change this:

```css
.one {
  order: 3;
}

.two {
  order: 1;
}

.three {
  order: 2;
}
```

The visual order becomes:

```text
2 → 3 → 1
```

The default value is:

```css
order: 0;
```

Items with lower `order` values appear before items with higher values.

However, `order` should be used carefully.

Changing visual order with CSS does not necessarily change the logical DOM order used by assistive technologies and keyboard navigation. For accessibility, the HTML structure should usually reflect the intended logical reading order.

---

# **e) `justify-content` vs. `align-items`**

One of the most common Flexbox mistakes is thinking:

```text
justify-content = horizontal
align-items     = vertical
```

This is only true when:

```css
flex-direction: row;
```

The correct rule is:

```text
justify-content → Main axis
align-items     → Cross axis
```

For example:

```css
.container {
  display: flex;
  flex-direction: row;

  justify-content: center;
  align-items: center;
}
```

With `row`:

```text
Main axis  → Horizontal
Cross axis → Vertical
```

Therefore:

```text
justify-content → Horizontal
align-items     → Vertical
```

However:

```css
.container {
  display: flex;
  flex-direction: column;

  justify-content: center;
  align-items: center;
}
```

Now:

```text
Main axis  → Vertical
Cross axis → Horizontal
```

Therefore:

```text
justify-content → Vertical
align-items     → Horizontal
```

A better mental model is always:

```text
             FLEXBOX

             Main Axis
                 │
                 └── justify-content

             Cross Axis
                 │
                 └── align-items
```

---

# **f) Practical Example: Navigation Bar**

Flexbox is commonly used to create navigation bars.

HTML:

```html
<nav class="navbar">
  <div class="logo">MyWebsite</div>

  <div class="nav-links">
    <a href="#">Home</a>
    <a href="#">Projects</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </div>
</nav>
```

CSS:

```css
.navbar {
  display: flex;

  justify-content: space-between;
  align-items: center;

  padding: 20px;
}

.nav-links {
  display: flex;
  gap: 20px;
}
```

Notice that `.navbar` is a flex container.

Its children are:

```text
.logo
.nav-links
```

At the same time, `.nav-links` is **also a flex container** for the individual `<a>` elements.

This creates nested Flexbox layouts:

```text
navbar
│
├── logo
│
└── nav-links
    │
    ├── Home
    ├── Projects
    ├── About
    └── Contact
```

This pattern is extremely common in modern web development.

---

# **g) Practical Example: Responsive Cards**

Flexbox can also create responsive groups of cards.

HTML:

```html
<section class="cards">
  <article class="card">
    <h2>HTML</h2>
    <p>Structure of the web.</p>
  </article>

  <article class="card">
    <h2>CSS</h2>
    <p>Presentation of the web.</p>
  </article>

  <article class="card">
    <h2>JavaScript</h2>
    <p>Behavior of the web.</p>
  </article>
</section>
```

CSS:

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 250px;

  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
}
```

The important declaration is:

```css
.card {
  flex: 1 1 250px;
}
```

This means:

```text
flex-grow:   1
flex-shrink: 1
flex-basis:  250px
```

The cards:

- Start with a preferred size of approximately `250px`.
- Can grow if additional space is available.
- Can shrink if necessary.
- Can move to another line because the parent uses `flex-wrap: wrap`.

This creates a simple responsive layout without requiring many media queries.

---

# **h) Flexbox and Responsive Design**

Flexbox is particularly useful for responsive interfaces because the browser can dynamically distribute available space.

For example:

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.item {
  flex: 1 1 300px;
}
```

On a large screen, several items may appear in one row.

```text
[ Item ] [ Item ] [ Item ]
```

As the viewport becomes smaller, the items can automatically wrap:

```text
[ Item ] [ Item ]

[ Item ]
```

And on an even smaller screen:

```text
[ Item ]

[ Item ]

[ Item ]
```

Flexbox therefore works particularly well for components such as:

- Navigation bars
- Toolbars
- Form controls
- Cards
- Button groups
- Sidebars
- Headers
- Footers
- Menus
- Small responsive layouts

---

# **i) Flexbox vs. CSS Grid**

Flexbox and CSS Grid are both powerful layout systems, but they are designed for somewhat different purposes.

### **Flexbox**

Flexbox is primarily **one-dimensional**.

It is ideal when controlling items mainly along:

```text
one row
```

or:

```text
one column
```

For example:

```text
Navigation bar

Logo       Home Projects About Contact
```

---

### **CSS Grid**

CSS Grid is primarily **two-dimensional**.

It is ideal when controlling both rows and columns simultaneously.

For example:

```text
┌────────┬────────┬────────┐
│ Card 1 │ Card 2 │ Card 3 │
├────────┼────────┼────────┤
│ Card 4 │ Card 5 │ Card 6 │
└────────┴────────┴────────┘
```

A simplified rule of thumb is:

```text
Flexbox → One-dimensional layouts
Grid    → Two-dimensional layouts
```

However, the two systems are complementary rather than competitors.

A page may use CSS Grid for its overall structure and Flexbox inside individual components.

For example:

```text
CSS Grid
│
├── Header
│    └── Flexbox navigation
│
├── Main content
│    └── Grid cards
│         └── Flexbox inside each card
│
└── Footer
     └── Flexbox links
```

---

# **j) Common Flexbox Patterns**

## **Equal-width Elements**

```css
.container {
  display: flex;
}

.item {
  flex: 1;
}
```

---

## **Elements with Consistent Spacing**

```css
.container {
  display: flex;
  gap: 1rem;
}
```

---

## **Center an Element**

```css
.container {
  display: flex;

  justify-content: center;
  align-items: center;
}
```

---

## **Push One Element to the Right**

Flexbox margins can absorb available space.

HTML:

```html
<nav class="navbar">
  <a href="#">Home</a>
  <a href="#">Projects</a>

  <a class="login" href="#">Login</a>
</nav>
```

CSS:

```css
.navbar {
  display: flex;
  gap: 20px;
}

.login {
  margin-left: auto;
}
```

Result:

```text
Home   Projects                    Login
```

This is an extremely useful Flexbox technique.

---

## **Responsive Cards**

```css
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 250px;
}
```

---

## **Fixed Sidebar + Flexible Content**

HTML:

```html
<div class="layout">
  <aside class="sidebar">Sidebar</aside>

  <main class="content">Main Content</main>
</div>
```

CSS:

```css
.layout {
  display: flex;
}

.sidebar {
  flex: 0 0 250px;
}

.content {
  flex: 1;
}
```

Here:

```css
.sidebar {
  flex: 0 0 250px;
}
```

means:

```text
Do not grow
Do not shrink
Start at 250px
```

while:

```css
.content {
  flex: 1;
}
```

allows the main content to occupy the remaining available space.

---

# **k) Common Mistakes**

### **1. Forgetting `display: flex`**

Flexbox properties such as:

```css
justify-content: center;
align-items: center;
```

will not create a Flexbox layout by themselves.

The parent element first needs:

```css
display: flex;
```

---

### **2. Applying Container Properties to Flex Items**

This will usually not produce the intended result:

```css
.item {
  justify-content: center;
}
```

unless `.item` is itself also a flex container.

Remember:

```text
justify-content
align-items
flex-direction
flex-wrap
gap
```

normally belong to the **flex container**.

Meanwhile:

```text
flex-grow
flex-shrink
flex-basis
align-self
order
```

belong to the **flex items**.

---

### **3. Thinking `justify-content` Always Means Horizontal**

Incorrect mental model:

```text
justify-content = horizontal
align-items = vertical
```

Better mental model:

```text
justify-content = main axis
align-items = cross axis
```

---

### **4. Confusing `align-items` and `align-content`**

```text
align-items
→ Aligns items inside each flex line.

align-content
→ Distributes multiple flex lines.
```

`align-content` only becomes relevant when the layout has multiple lines, usually because of:

```css
flex-wrap: wrap;
```

---

### **5. Overusing `order`**

Although `order` can visually rearrange elements, the logical structure of the HTML remains unchanged.

For accessibility and maintainability, it is usually better to place elements in the correct semantic order directly in the HTML whenever possible.

---

# **l) Flexbox Property Summary**

### **Flex Container**

```css
.container {
  display: flex;

  flex-direction: row;
  flex-wrap: nowrap;

  justify-content: flex-start;
  align-items: stretch;
  align-content: stretch;

  gap: 0;
}
```

### **Flex Item**

```css
.item {
  flex-grow: 0;
  flex-shrink: 1;
  flex-basis: auto;

  align-self: auto;
  order: 0;
}
```

A compact way to remember Flexbox is:

```text
CONTAINER
│
├── Direction
│   ├── flex-direction
│   └── flex-wrap
│
├── Main-axis alignment
│   └── justify-content
│
├── Cross-axis alignment
│   ├── align-items
│   └── align-content
│
└── Spacing
    └── gap


ITEM
│
├── Size behavior
│   ├── flex-grow
│   ├── flex-shrink
│   └── flex-basis
│
├── Individual alignment
│   └── align-self
│
└── Visual order
    └── order
```

---

# **References**

- MDN Web Docs — _Basic concepts of Flexbox_ https://developer.mozilla.org/es/docs/Web/CSS/Guides/Flexible_box_layout/Basic_concepts#contenedores_flex_multi-l%C3%ADnea_con_flex-wrap
- https://www.aulacreactiva.com/flexbox-herramienta-diseno-web/
- MDN Web Docs — _Aligning items in a flex container_
- CSS-Tricks — _A Complete Guide to Flexbox_ https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- web.dev— _CSS Flexible Box Layout Module Level 1_ https://web.dev/learn/css/flexbox?hl=es
