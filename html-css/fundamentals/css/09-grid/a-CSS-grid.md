# **12. CSS Grid 🧩**

**CSS Grid Layout**, commonly called **CSS Grid** or simply **Grid**, is a two-dimensional CSS layout system designed specifically for arranging elements into **rows and columns**.

Before modern layout systems such as Grid and Flexbox, developers often relied on techniques such as tables, floats, `inline-block`, and positioning to create page layouts. These approaches were not originally designed for complex webpage layouts and often required workarounds. CSS Grid was created specifically to provide a native CSS system for building structured layouts.

Grid is especially powerful because it allows developers to control:

- Rows and columns simultaneously
- Track sizes
- Element placement
- Spacing
- Alignment
- Responsive behavior
- Named layout areas
- Automatically generated rows and columns
- Overlapping elements

A grid is essentially a collection of intersecting horizontal and vertical lines. One set defines the **rows**, while the other defines the **columns**. Elements can then be positioned relative to those rows, columns, lines, cells, or larger areas.

A very simple Grid layout looks like this:

```html
<div class="grid">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```

The result can be imagined as:

```text
┌───────────┬───────────┐
│     1     │     2     │
├───────────┼───────────┤
│     3     │     4     │
└───────────┴───────────┘
```

Unlike **Flexbox**, which primarily manages layout in one dimension at a time, Grid is designed for **two-dimensional layouts**. This means it can control rows and columns simultaneously.

A useful mental model is:

```text
Flexbox → one-dimensional layout
          row OR column

Grid    → two-dimensional layout
          rows AND columns
```

However, Grid and Flexbox are not competitors. They are complementary tools and are frequently used together.

---

# **a) Grid Containers**

A **grid container** is the element on which Grid layout is activated.

To create one, use:

```css
.container {
  display: grid;
}
```

or:

```css
.container {
  display: inline-grid;
}
```

Once `display: grid` is applied, every **direct child** of that element becomes a **grid item**.

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
  display: grid;
}
```

Here:

```text
.container
│
├── Apple
├── Pear
└── Orange
```

`.container` is the **grid container**, while the three `<div>` elements are **grid items**.

---

## **`grid` vs. `inline-grid`**

Both values create a grid formatting context for their children.

The main difference is how the container itself behaves relative to surrounding content.

```css
.container {
  display: grid;
}
```

creates a block-level grid container.

```css
.container {
  display: inline-grid;
}
```

creates an inline-level grid container.

Conceptually:

```text
display: grid
→ Grid behaves similarly to a block-level element.

display: inline-grid
→ Grid participates in inline flow.
```

The internal Grid behavior remains essentially the same.

---

# **b) Grid Items**

A **grid item** is a direct child of a grid container.

For example:

```html
<div class="grid">
  <article>Item 1</article>
  <article>Item 2</article>
  <article>Item 3</article>
</div>
```

```css
.grid {
  display: grid;
}
```

The three `<article>` elements become grid items.

However, nested elements are **not automatically grid items**.

```html
<div class="grid">
  <article class="card">
    <h2>CSS Grid</h2>
    <p>Two-dimensional layouts.</p>
  </article>
</div>
```

Here:

```text
.grid    → Grid container
.card    → Grid item
<h2>     → Normal child of .card
<p>      → Normal child of .card
```

If `.card` also needs to arrange its own children using Grid, it can become another grid container:

```css
.card {
  display: grid;
}
```

An element can therefore simultaneously be:

```text
A grid item      → relative to its parent
A grid container → relative to its children
```

---

# **c) Grid Terminology**

Understanding Grid terminology is essential because Grid properties are based around concepts such as **tracks**, **lines**, **cells**, and **areas**.

The main Grid concepts are:

```text
Grid Container
Grid Item
Grid Line
Grid Track
Grid Cell
Grid Area
Grid Gap
```

These concepts are described throughout the CSS Grid documentation from MDN, CSS-Tricks, web.dev, and LenguajeCSS.

Consider the following grid:

```text
       Column 1       Column 2       Column 3

    1             2             3             4
    │             │             │             │
1 ──┼─────────────┼─────────────┼─────────────┼──
    │             │             │             │
    │      A      │      B      │      C      │
    │             │             │             │
2 ──┼─────────────┼─────────────┼─────────────┼──
    │             │             │             │
    │      D      │      E      │      F      │
    │             │             │             │
3 ──┼─────────────┼─────────────┼─────────────┼──
```

This grid contains:

```text
3 columns
2 rows
4 vertical grid lines
3 horizontal grid lines
6 grid cells
```

---

# **d) Rows and Columns**

The fundamental structure of CSS Grid consists of **rows and columns**.

A column runs vertically:

```text
COLUMN

┌───────┐
│       │
│       │
│       │
│       │
└───────┘
```

A row runs horizontally:

```text
ROW

┌───────────────────────────────┐
│                               │
└───────────────────────────────┘
```

Together, rows and columns form the grid:

```text
          Columns
       ↓       ↓       ↓

    ┌───────┬───────┬───────┐
 →  │       │       │       │
Row ├───────┼───────┼───────┤
 →  │       │       │       │
    └───────┴───────┴───────┘
```

The sizes of explicit columns and rows are usually defined using:

```css
grid-template-columns
grid-template-rows
```

---

# **e) Grid Lines**

**Grid lines** are the horizontal and vertical boundaries separating the tracks of a grid.

If a Grid has three columns:

```text
Line 1      Line 2      Line 3      Line 4
  │           │           │           │
  │ Column 1  │ Column 2  │ Column 3  │
  │           │           │           │
```

Notice an important detail:

```text
3 columns → 4 column lines
```

Similarly:

```text
2 rows → 3 row lines
```

Grid lines are numbered starting from `1`, and they can be used to precisely position Grid items. Their numbering follows the document's writing mode, so the physical direction of line `1` is not universally equivalent to "left."

For a typical left-to-right English document:

```text
1        2        3        4
│        │        │        │
├────────┼────────┼────────┤
```

An element can be placed between particular grid lines:

```css
.item {
  grid-column-start: 1;
  grid-column-end: 3;
}
```

This means:

```text
Start at column line 1
End at column line 3
```

Therefore, the item occupies **two column tracks**.

---

# **f) Grid Tracks**

A **grid track** is the space between two adjacent grid lines.

Tracks are effectively the rows and columns of the grid.

For example:

```text
Line 1         Line 2         Line 3
  │              │              │
  │   Track 1    │   Track 2    │
  │              │              │
```

A vertical track is a **column track**.

A horizontal track is a **row track**.

Grid tracks can use:

- Fixed dimensions
- Percentages
- Flexible fractions
- Intrinsic sizing
- Minimum and maximum sizes

For example:

```css
.grid {
  display: grid;

  grid-template-columns:
    200px
    1fr
    2fr;
}
```

This creates three column tracks.

---

# **g) Grid Cells**

A **grid cell** is the smallest individual unit of a grid.

It is created where one row and one column intersect. MDN compares it conceptually to a table cell.

For example:

```text
┌────────────┬────────────┐
│   Cell 1   │   Cell 2   │
├────────────┼────────────┤
│   Cell 3   │   Cell 4   │
└────────────┴────────────┘
```

By default, auto-placed Grid items normally occupy one cell each unless their placement or span is changed.

---

# **h) Grid Areas**

A **grid area** is a rectangular region of the grid composed of one or more grid cells.

For example:

```text
┌─────────────────────────┐
│                         │
│       GRID AREA         │
│                         │
├────────────┬────────────┤
│            │            │
└────────────┴────────────┘
```

An area can span:

- Several columns
- Several rows
- Both rows and columns

Grid areas must remain rectangular; they cannot form arbitrary shapes such as an L-shaped region.

Grid areas can be created using line placement or using named areas with:

```css
grid-template-areas
```

---

# **i) `grid-template-columns`**

The `grid-template-columns` property defines the number and size of columns in the **explicit grid**.

For example:

```css
.grid {
  display: grid;
  grid-template-columns: 150px 300px;
}
```

This creates:

```text
Column 1 → 150px
Column 2 → 300px
```

Conceptually:

```text
┌───────────┬────────────────────┐
│   150px   │       300px        │
└───────────┴────────────────────┘
```

This behavior is described in the LenguajeCSS Grid guide and MDN's Grid documentation.

You can mix different units:

```css
.grid {
  grid-template-columns: 200px 30% 1fr;
}
```

Or use content-aware sizing:

```css
.grid {
  grid-template-columns: auto 1fr;
}
```

---

# **j) `grid-template-rows`**

`grid-template-rows` defines the size of explicitly created rows.

For example:

```css
.grid {
  display: grid;

  grid-template-columns: 200px 200px;
  grid-template-rows: 100px 250px;
}
```

The grid becomes:

```text
                 200px       200px

              ┌───────────┬───────────┐
     100px    │           │           │
              ├───────────┼───────────┤
     250px    │           │           │
              │           │           │
              └───────────┴───────────┘
```

The first row is `100px` tall.

The second row is `250px` tall.

---

# **k) The `fr` Unit**

CSS Grid introduces the **fractional unit**, written as:

```css
fr
```

`fr` represents a fraction of the available space inside the grid container.

For example:

```css
.grid {
  display: grid;

  grid-template-columns: 1fr 1fr 1fr;
}
```

The available space is divided equally:

```text
┌────────────┬────────────┬────────────┐
│    1fr     │    1fr     │    1fr     │
└────────────┴────────────┴────────────┘
```

Each column receives approximately one third of the distributable space.

---

## **Different Fractions**

```css
.grid {
  grid-template-columns: 1fr 2fr 1fr;
}
```

The available space is divided into four fractional portions:

```text
1 + 2 + 1 = 4
```

Therefore:

```text
Column 1 → 1/4
Column 2 → 2/4
Column 3 → 1/4
```

Conceptually:

```text
┌───────┬──────────────┬───────┐
│  1fr  │     2fr      │  1fr  │
└───────┴──────────────┴───────┘
```

---

## **Mixing Fixed and Flexible Units**

You can combine `fr` with other sizing units:

```css
.grid {
  grid-template-columns: 250px 1fr 2fr;
}
```

The `250px` column is allocated first, and the remaining distributable space is shared by the flexible tracks.

This pattern is useful for layouts such as:

```text
Sidebar + Main Content + Secondary Content
```

---

# **l) The `repeat()` Function**

When several tracks use the same size, repeating the same value manually becomes unnecessary.

Instead of:

```css
.grid {
  grid-template-columns:
    1fr
    1fr
    1fr
    1fr;
}
```

we can use:

```css
.grid {
  grid-template-columns: repeat(4, 1fr);
}
```

The syntax is:

```css
repeat(number-of-repetitions, track-definition)
```

For example:

```css
.grid {
  grid-template-columns:
    100px
    repeat(3, 1fr)
    200px;
}
```

is conceptually equivalent to:

```css
.grid {
  grid-template-columns:
    100px
    1fr
    1fr
    1fr
    200px;
}
```

`repeat()` can also repeat more complicated patterns.

For example:

```css
.grid {
  grid-template-columns: repeat(2, 1fr 2fr);
}
```

is equivalent to:

```css
.grid {
  grid-template-columns: 1fr 2fr 1fr 2fr;
}
```

---

# **m) The `minmax()` Function**

The `minmax()` function defines a track size with both a minimum and maximum value.

Its syntax is:

```css
minmax(minimum, maximum)
```

For example:

```css
.grid {
  grid-template-columns: repeat(3, minmax(200px, 1fr));
}
```

Each column should be at least:

```text
200px
```

but it may grow to consume available space:

```text
1fr
```

Conceptually:

```text
Minimum size → 200px
Maximum size → flexible fraction
```

This is extremely useful for responsive layouts.

---

# **n) `auto-fill` and `auto-fit`**

One of the most powerful Grid patterns combines:

```css
repeat()
minmax()
auto-fit
```

For example:

```css
.cards {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 1rem;
}
```

This tells the browser to create as many columns as can fit while keeping each column at least `250px` wide.

When more space becomes available, the tracks can expand.

This pattern can create highly responsive interfaces with little or no media-query logic. LenguajeCSS describes the combination of `repeat()`, `minmax()`, and `auto-fill`/`auto-fit` as a way to adapt tracks to the available viewport width.

---

## **`auto-fill`**

For example:

```css
.grid {
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

`auto-fill` attempts to create as many tracks of the specified size as can fit inside the container.

---

## **`auto-fit`**

```css
.grid {
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

`auto-fit` behaves similarly, but empty repeated tracks can collapse, allowing existing tracks to stretch and use the remaining space.

A useful practical pattern is:

```css
.cards {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 1.5rem;
}
```

This is commonly used for responsive card layouts.

---

# **o) Grid Gaps**

The space between rows and columns is sometimes called a **gutter** or **gap**.

Grid provides three main properties:

```css
row-gap
column-gap
gap
```

MDN describes gutters as spaces between Grid cells created by `row-gap`, `column-gap`, or their shorthand `gap`.

For example:

```css
.grid {
  display: grid;

  grid-template-columns: repeat(3, 1fr);

  column-gap: 30px;
  row-gap: 15px;
}
```

Instead of defining them separately:

```css
column-gap: 30px;
row-gap: 15px;
```

we can use:

```css
gap: 15px 30px;
```

The first value represents the row gap:

```text
15px
```

The second represents the column gap:

```text
30px
```

If both are the same:

```css
.grid {
  gap: 20px;
}
```

---

## **Why Use `gap` Instead of Margins?**

Using:

```css
gap: 20px;
```

is usually preferable when the desired spacing is specifically between Grid items because the container controls the spacing directly.

For example:

```css
.cards {
  display: grid;
  gap: 1.5rem;
}
```

is generally cleaner than manually assigning margins to every card.

---

# **p) Explicit vs. Implicit Grid**

CSS Grid contains two related concepts:

```text
Explicit Grid
Implicit Grid
```

Understanding their difference is important when working with dynamically generated content.

---

## **Explicit Grid**

The **explicit grid** consists of rows and columns that you define directly using properties such as:

```css
grid-template-columns
grid-template-rows
```

For example:

```css
.grid {
  display: grid;

  grid-template-columns: repeat(3, 1fr);

  grid-template-rows: 100px 200px;
}
```

This explicitly defines:

```text
3 columns
2 rows
```

---

## **Implicit Grid**

If additional items require rows or columns that were not explicitly defined, Grid can automatically create new tracks.

These additional tracks form the **implicit grid**.

For example:

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

Suppose the container contains:

```html
<div class="grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```

We explicitly created three columns, but we did not explicitly define rows.

Grid automatically creates rows as necessary:

```text
┌───────┬───────┬───────┐
│   1   │   2   │   3   │
├───────┼───────┼───────┤
│   4   │   5   │   6   │ ← implicit row
└───────┴───────┴───────┘
```

---

# **q) `grid-auto-rows` and `grid-auto-columns`**

Implicit tracks can be sized using:

```css
grid-auto-rows
grid-auto-columns
```

For example:

```css
.grid {
  display: grid;

  grid-template-columns: repeat(3, 1fr);

  grid-auto-rows: 150px;
}
```

Every automatically generated row will be `150px` tall.

A more flexible version is:

```css
.grid {
  grid-auto-rows: minmax(100px, auto);
}
```

This means implicit rows should have:

```text
minimum → 100px
maximum → enough space for content
```

---

# **r) Grid Placement**

One of Grid's most powerful features is the ability to place elements at precise positions.

Elements can be positioned using:

```css
grid-column-start
grid-column-end

grid-row-start
grid-row-end
```

For example:

```css
.featured {
  grid-column-start: 1;
  grid-column-end: 3;
}
```

The element begins at column line `1` and ends at column line `3`.

Therefore:

```text
Line 1       Line 2       Line 3

│────────────── ITEM ──────────────│
```

Grid positioning fundamentally targets **grid lines**, not cells or column numbers directly.

---

# **s) `grid-column` and `grid-row`**

Instead of writing:

```css
.item {
  grid-column-start: 1;
  grid-column-end: 3;
}
```

we can use the shorthand:

```css
.item {
  grid-column: 1 / 3;
}
```

Similarly:

```css
.item {
  grid-row: 2 / 4;
}
```

means:

```text
Start at row line 2
End at row line 4
```

A complete example:

```css
.item {
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
```

This element spans:

```text
2 columns
2 rows
```

---

# **t) The `span` Keyword**

Instead of specifying the ending line directly, Grid lets us specify how many tracks an item should span.

For example:

```css
.item {
  grid-column: span 2;
}
```

This means:

```text
Occupy 2 columns
```

Similarly:

```css
.item {
  grid-row: span 3;
}
```

means:

```text
Occupy 3 rows
```

A common card layout might use:

```css
.featured-card {
  grid-column: span 2;
}
```

---

# **u) Negative Grid Line Numbers**

Grid lines can also be referenced using negative numbers.

For example:

```css
.header {
  grid-column: 1 / -1;
}
```

`-1` refers to the final line of the explicit grid.

Therefore:

```css
grid-column: 1 / -1;
```

is a common way to make an element span the entire explicit grid width.

For example:

```text
┌──────────────────────────────┐
│            HEADER            │
├─────────┬─────────┬──────────┤
│         │         │          │
└─────────┴─────────┴──────────┘
```

---

# **v) Grid Areas**

Grid also allows developers to create **named areas**, making complex layouts easier to read.

Suppose we want:

```text
┌──────────────────────────────┐
│            Header            │
├──────────┬───────────────────┤
│ Sidebar  │       Main        │
├──────────┴───────────────────┤
│            Footer            │
└──────────────────────────────┘
```

HTML:

```html
<div class="layout">
  <header class="header">Header</header>

  <aside class="sidebar">Sidebar</aside>

  <main class="main">Main Content</main>

  <footer class="footer">Footer</footer>
</div>
```

First, assign names to the Grid items:

```css
.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.main {
  grid-area: main;
}

.footer {
  grid-area: footer;
}
```

Then define the layout:

```css
.layout {
  display: grid;

  grid-template-columns: 250px 1fr;

  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
}
```

This produces a declarative representation of the page layout. Named Grid areas are particularly useful for page structures and make the relationship between CSS and the visual design easy to understand.

---

## **Understanding `grid-template-areas`**

Consider:

```css
grid-template-areas:
  "header header"
  "sidebar main"
  "footer footer";
```

Each quoted line represents a row:

```text
"header header"
```

means:

```text
┌──────────────────────────────┐
│            header            │
└──────────────────────────────┘
```

The next line:

```text
"sidebar main"
```

becomes:

```text
┌──────────────┬───────────────┐
│   sidebar    │     main      │
└──────────────┴───────────────┘
```

---

## **Empty Grid Areas**

A period can represent an unused cell:

```css
grid-template-areas:
  "header header"
  "sidebar main"
  ". footer";
```

Conceptually:

```text
┌─────────┬─────────┐
│ header  │ header  │
├─────────┼─────────┤
│ sidebar │ main    │
├─────────┼─────────┤
│  empty  │ footer  │
└─────────┴─────────┘
```

---

# **w) Grid Alignment**

CSS Grid provides extensive alignment controls.

A useful distinction is:

```text
justify-* → inline/row direction
align-*   → block/column direction
```

The most important Grid alignment properties include:

```css
justify-items
align-items
place-items

justify-content
align-content
place-content

justify-self
align-self
place-self
```

Grid uses CSS Box Alignment features to control both the placement of individual items and the placement of the Grid itself.

---

# **x) `justify-items`**

`justify-items` aligns grid items inside their individual grid areas along the inline axis.

For example:

```css
.grid {
  display: grid;
  justify-items: center;
}
```

Common values include:

```css
justify-items: stretch;
justify-items: start;
justify-items: center;
justify-items: end;
```

The default is normally:

```css
justify-items: stretch;
```

for Grid items when appropriate.

---

# **y) `align-items`**

`align-items` controls Grid item alignment along the block axis.

For example:

```css
.grid {
  display: grid;
  align-items: center;
}
```

Common values:

```css
align-items: stretch;
align-items: start;
align-items: center;
align-items: end;
```

---

# **z) `place-items`**

`place-items` is a shorthand for:

```text
align-items
+
justify-items
```

Instead of:

```css
.grid {
  align-items: center;
  justify-items: center;
}
```

we can write:

```css
.grid {
  place-items: center;
}
```

This is particularly useful for centering content inside Grid cells.

For example:

```css
.card {
  display: grid;
  place-items: center;
}
```

---

# **aa) `justify-content` and `align-content`**

These properties align the **entire Grid** inside the Grid container when the Grid itself is smaller than the available container space.

For example:

```css
.grid {
  display: grid;

  grid-template-columns: 100px 100px;

  width: 500px;

  justify-content: center;
}
```

The columns occupy only:

```text
200px
```

inside a:

```text
500px
```

container, so `justify-content` controls the distribution of the remaining space.

Common values include:

```css
start
end
center
stretch
space-between
space-around
space-evenly
```

---

# **ab) `justify-self` and `align-self`**

These properties allow a single Grid item to override the container's default item alignment.

For example:

```css
.grid {
  justify-items: stretch;
}
```

But:

```css
.special {
  justify-self: center;
}
```

centers only the `.special` item.

Similarly:

```css
.special {
  align-self: end;
}
```

---

# **ac) Auto-Placement**

CSS Grid includes an **auto-placement algorithm**.

This means Grid can automatically position items for which no explicit position has been specified.

For example:

```html
<div class="grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

Grid automatically produces approximately:

```text
┌─────┬─────┬─────┐
│  1  │  2  │  3  │
├─────┼─────┼─────┤
│  4  │  5  │  6  │
└─────┴─────┴─────┘
```

No individual placement properties are necessary.

---

# **ad) `grid-auto-flow`**

`grid-auto-flow` controls how auto-placed items are inserted into the Grid.

The default behavior is approximately:

```css
grid-auto-flow: row;
```

which fills rows first.

```text
1 → 2 → 3
4 → 5 → 6
```

You can instead use:

```css
grid-auto-flow: column;
```

which fills columns first.

You may also encounter:

```css
grid-auto-flow: dense;
```

The `dense` packing mode attempts to fill earlier gaps when smaller items can fit.

However, it should be used carefully because the visual order can differ from the source order.

---

# **ae) Responsive Grid Without Media Queries**

One of the most practical Grid patterns is:

```css
.grid {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 1.5rem;
}
```

Suppose the HTML contains:

```html
<section class="grid">
  <article class="card">1</article>
  <article class="card">2</article>
  <article class="card">3</article>
  <article class="card">4</article>
</section>
```

On a large screen, the layout might become:

```text
┌────────┬────────┬────────┬────────┐
│   1    │   2    │   3    │   4    │
└────────┴────────┴────────┴────────┘
```

On a medium screen:

```text
┌────────────┬────────────┐
│     1      │     2      │
├────────────┼────────────┤
│     3      │     4      │
└────────────┴────────────┘
```

On a narrow screen:

```text
┌─────────────────────────┐
│            1            │
├─────────────────────────┤
│            2            │
├─────────────────────────┤
│            3            │
├─────────────────────────┤
│            4            │
└─────────────────────────┘
```

All of this can happen without explicitly defining the number of columns for every viewport width.

---

# **af) Grid and Media Queries**

Grid also works extremely well with media queries.

For example:

```css
.layout {
  display: grid;

  grid-template-columns: 1fr;

  grid-template-areas:
    "header"
    "main"
    "sidebar"
    "footer";
}
```

Then, for larger screens:

```css
@media (min-width: 768px) {
  .layout {
    grid-template-columns: 250px 1fr;

    grid-template-areas:
      "header  header"
      "sidebar main"
      "footer  footer";
  }
}
```

The HTML does not need to change.

Grid simply reorganizes the same semantic elements according to the available screen size.

This is one of the strongest advantages of named Grid areas.

---

# **ag) Grid Shorthand**

CSS Grid provides several shorthand properties.

For example:

```css
grid-template
```

can combine:

```css
grid-template-rows
grid-template-columns
```

A basic form is:

```css
grid-template: rows / columns;
```

For example:

```css
.grid {
  display: grid;

  grid-template:
    100px 200px /
    1fr 2fr;
}
```

This corresponds roughly to:

```css
.grid {
  display: grid;

  grid-template-rows: 100px 200px;

  grid-template-columns: 1fr 2fr;
}
```

LenguajeCSS describes `grid-template` as a shorthand for defining the dimensions of the explicit grid.

For beginners, however, writing the longhand properties can sometimes make the layout easier to understand.

---

# **ah) Grid Item Overlap**

Unlike traditional document flow, multiple Grid items can occupy overlapping areas.

MDN specifically notes that Grid allows elements to overlap and that their layering can be controlled using `z-index`.

For example:

```html
<div class="hero">
  <img class="hero-image" src="image.jpg" alt="" />

  <div class="hero-content">
    <h1>Hello!</h1>
  </div>
</div>
```

```css
.hero {
  display: grid;
}

.hero-image,
.hero-content {
  grid-column: 1;
  grid-row: 1;
}
```

Both items occupy the same Grid area.

Then:

```css
.hero-content {
  z-index: 1;
}
```

can place the content above the image.

This technique can be useful for:

- Hero sections
- Text overlays
- Image captions
- Layered UI elements

---

# **ai) Grid vs. Flexbox**

Grid and Flexbox are both modern layout systems, but they solve different kinds of problems.

## **Flexbox**

Flexbox is primarily one-dimensional.

```text
Row

[A] [B] [C] [D]
```

or:

```text
Column

[A]
[B]
[C]
[D]
```

It is particularly useful when the relationship between items along one axis is the main concern.

Examples:

- Navigation bars
- Button groups
- Toolbars
- Component alignment
- Centering elements

---

## **Grid**

Grid is two-dimensional.

```text
┌─────┬─────┬─────┐
│  A  │  B  │  C  │
├─────┼─────┼─────┤
│  D  │  E  │  F  │
└─────┴─────┴─────┘
```

It is especially useful when both rows and columns matter.

Examples:

- Page layouts
- Dashboards
- Galleries
- Card collections
- Complex responsive layouts

CSS-Tricks and web.dev both emphasize this distinction: Flexbox primarily handles one-dimensional flow, while Grid is designed for two-dimensional layouts.

A useful rule of thumb is:

```text
Need to arrange items mostly
in one direction?

→ Consider Flexbox.

Need to control rows and
columns together?

→ Consider Grid.
```

But many real interfaces combine both.

---

# **aj) Combining Grid and Flexbox**

Suppose Grid controls the main page layout:

```css
.page {
  display: grid;

  grid-template-columns: 250px 1fr;

  grid-template-areas: "sidebar main";
}
```

Inside the main area, Flexbox can control a navigation component:

```css
.navbar {
  display: flex;

  justify-content: space-between;

  align-items: center;
}
```

Conceptually:

```text
GRID
│
├── Sidebar
│
└── Main
     │
     ├── FLEXBOX navbar
     │
     └── GRID cards
```

This is common in production interfaces.

---

# **ak) Practical Example: Card Grid**

HTML:

```html
<section class="cards">
  <article class="card">
    <h2>HTML</h2>
    <p>Defines webpage structure.</p>
  </article>

  <article class="card">
    <h2>CSS</h2>
    <p>Defines webpage presentation.</p>
  </article>

  <article class="card">
    <h2>JavaScript</h2>
    <p>Adds logic and interaction.</p>
  </article>

  <article class="card">
    <h2>React</h2>
    <p>Builds component-based interfaces.</p>
  </article>
</section>
```

CSS:

```css
.cards {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 1.5rem;
}

.card {
  padding: 1.5rem;

  border: 1px solid #ccc;

  border-radius: 0.75rem;
}
```

This layout is flexible because Grid automatically determines how many cards can fit in each row.

---

# **al) Practical Example: Dashboard**

HTML:

```html
<div class="dashboard">
  <header class="header">Dashboard</header>

  <aside class="sidebar">Navigation</aside>

  <main class="main">Main Content</main>

  <section class="stats">Statistics</section>

  <footer class="footer">Footer</footer>
</div>
```

CSS:

```css
.dashboard {
  display: grid;

  min-height: 100vh;

  grid-template-columns: 220px 1fr 300px;

  grid-template-rows: auto 1fr auto;

  grid-template-areas:
    "header  header header"
    "sidebar main   stats"
    "footer  footer footer";

  gap: 1rem;
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.main {
  grid-area: main;
}

.stats {
  grid-area: stats;
}

.footer {
  grid-area: footer;
}
```

Conceptually:

```text
┌───────────────────────────────────┐
│              HEADER               │
├──────────┬──────────────┬─────────┤
│ SIDEBAR  │     MAIN     │  STATS  │
│          │              │         │
│          │              │         │
├──────────┴──────────────┴─────────┤
│              FOOTER               │
└───────────────────────────────────┘
```

---

# **am) Practical Example: Article Layout**

Grid is also useful for layouts where some elements span multiple columns.

HTML:

```html
<main class="articles">
  <article class="featured">Featured Article</article>

  <article>Article 2</article>

  <article>Article 3</article>

  <article>Article 4</article>
</main>
```

CSS:

```css
.articles {
  display: grid;

  grid-template-columns: repeat(3, 1fr);

  gap: 1.5rem;
}

.featured {
  grid-column: span 2;

  grid-row: span 2;
}
```

This creates an editorial-style layout where the featured article receives more visual space.

---

# **an) Common Grid Patterns**

## **Equal Columns**

```css
.grid {
  display: grid;

  grid-template-columns: repeat(3, 1fr);
}
```

---

## **Fixed Sidebar + Flexible Content**

```css
.layout {
  display: grid;

  grid-template-columns: 250px 1fr;
}
```

---

## **Responsive Cards**

```css
.cards {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));

  gap: 1rem;
}
```

---

## **Full-Width Header**

```css
.header {
  grid-column: 1 / -1;
}
```

---

## **Element Spanning Two Columns**

```css
.featured {
  grid-column: span 2;
}
```

---

## **Center Content Inside Grid Cells**

```css
.grid {
  display: grid;
  place-items: center;
}
```

---

## **Page Layout with Named Areas**

```css
.page {
  display: grid;

  grid-template-areas:
    "header header"
    "aside  main"
    "footer footer";
}
```

---

# **ao) Common Mistakes**

## **1. Forgetting `display: grid`**

Properties such as:

```css
grid-template-columns: repeat(3, 1fr);
```

will not create a Grid layout unless the parent establishes a Grid formatting context:

```css
.container {
  display: grid;
}
```

---

## **2. Confusing Grid Lines with Columns**

Suppose we have:

```css
grid-template-columns: repeat(3, 1fr);
```

This produces:

```text
3 columns
4 column lines
```

Therefore:

```css
grid-column: 1 / 3;
```

does **not** mean:

```text
Column 1 through column 3
```

Instead it means:

```text
Start at line 1
End at line 3
```

which occupies two tracks.

---

## **3. Thinking `fr` Is Simply a Percentage**

This:

```css
grid-template-columns: 1fr 1fr 1fr;
```

does not literally mean:

```text
33.333% 33.333% 33.333%
```

`fr` distributes available Grid space after relevant sizing considerations such as fixed tracks and gaps have been accounted for. MDN specifically describes `fr` as representing a fraction of the available space in the Grid container.

---

## **4. Using Margins Instead of `gap`**

Instead of:

```css
.card {
  margin: 0 20px 20px 0;
}
```

prefer Grid's spacing mechanism when the goal is simply spacing between tracks:

```css
.grid {
  gap: 20px;
}
```

---

## **5. Defining Too Many Fixed Widths**

A layout such as:

```css
grid-template-columns: 300px 300px 300px 300px;
```

may overflow narrow screens.

A more responsive alternative could be:

```css
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```

---

## **6. Ignoring the Implicit Grid**

If more elements exist than the explicit Grid can accommodate, Grid may generate implicit tracks.

Understanding:

```css
grid-auto-rows
grid-auto-columns
```

helps control those generated tracks.

---

## **7. Using Grid When Flexbox Is Simpler**

Not every component needs two-dimensional layout.

For a simple navigation bar:

```text
Logo             Home About Contact
```

Flexbox may be simpler.

For an entire dashboard:

```text
Header
Sidebar | Main | Stats
Footer
```

Grid may be more appropriate.

Choose the system that best matches the layout problem.

---

# **ap) Grid Property Summary**

## **Properties Commonly Applied to the Grid Container**

```css
.container {
  display: grid;

  grid-template-columns: ...;

  grid-template-rows: ...;

  grid-template-areas: ...;

  grid-auto-columns: ...;

  grid-auto-rows: ...;

  grid-auto-flow: row;

  gap: ...;

  justify-items: ...;

  align-items: ...;

  place-items: ...;

  justify-content: ...;

  align-content: ...;

  place-content: ...;
}
```

---

## **Properties Commonly Applied to Grid Items**

```css
.item {
  grid-column-start: ...;

  grid-column-end: ...;

  grid-column: ...;

  grid-row-start: ...;

  grid-row-end: ...;

  grid-row: ...;

  grid-area: ...;

  justify-self: ...;

  align-self: ...;

  place-self: ...;
}
```

---

# **aq) Mental Model**

A useful way to organize CSS Grid concepts is:

```text
CSS GRID
│
├── Create the Grid
│   │
│   ├── display: grid
│   └── display: inline-grid
│
├── Define Structure
│   │
│   ├── grid-template-columns
│   ├── grid-template-rows
│   └── grid-template-areas
│
├── Size Tracks
│   │
│   ├── px
│   ├── %
│   ├── auto
│   ├── fr
│   ├── minmax()
│   └── repeat()
│
├── Responsive Tracks
│   │
│   ├── auto-fill
│   └── auto-fit
│
├── Space Tracks
│   │
│   ├── row-gap
│   ├── column-gap
│   └── gap
│
├── Place Items
│   │
│   ├── grid-column
│   ├── grid-row
│   ├── span
│   └── grid-area
│
├── Automatic Placement
│   │
│   ├── grid-auto-flow
│   ├── grid-auto-rows
│   └── grid-auto-columns
│
└── Alignment
    │
    ├── justify-items
    ├── align-items
    ├── place-items
    │
    ├── justify-content
    ├── align-content
    ├── place-content
    │
    ├── justify-self
    ├── align-self
    └── place-self
```

---

# **ar) Complete Example**

The following example combines many of the concepts introduced in this chapter.

### **HTML**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>CSS Grid Example</title>

    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div class="page">
      <header class="header">
        <h1>My Website</h1>
      </header>

      <aside class="sidebar">
        <nav>
          <a href="#">Home</a>
          <a href="#">Articles</a>
          <a href="#">Projects</a>
          <a href="#">About</a>
        </nav>
      </aside>

      <main class="main">
        <h2>CSS Topics</h2>

        <section class="cards">
          <article class="card featured">
            <h3>CSS Grid</h3>

            <p>A two-dimensional layout system for rows and columns.</p>
          </article>

          <article class="card">
            <h3>Flexbox</h3>

            <p>A one-dimensional layout system.</p>
          </article>

          <article class="card">
            <h3>Responsive Design</h3>

            <p>Interfaces that adapt to different screens.</p>
          </article>

          <article class="card">
            <h3>Animations</h3>

            <p>Motion and transitions using CSS.</p>
          </article>
        </section>
      </main>

      <footer class="footer">
        <p>Learning CSS 🍐</p>
      </footer>
    </div>
  </body>
</html>
```

### **CSS**

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;

  font-family: Arial, sans-serif;
}

.page {
  display: grid;

  min-height: 100vh;

  grid-template-columns: 220px 1fr;

  grid-template-rows: auto 1fr auto;

  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
}

.header {
  grid-area: header;

  padding: 1.5rem;
}

.sidebar {
  grid-area: sidebar;

  padding: 1.5rem;
}

.sidebar nav {
  display: grid;

  gap: 1rem;
}

.main {
  grid-area: main;

  padding: 2rem;
}

.cards {
  display: grid;

  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));

  gap: 1.5rem;
}

.card {
  padding: 1.5rem;

  border: 1px solid #ccc;

  border-radius: 0.75rem;
}

.featured {
  grid-column: span 2;
}

.footer {
  grid-area: footer;

  padding: 1.5rem;
}

@media (max-width: 700px) {
  .page {
    grid-template-columns: 1fr;

    grid-template-areas:
      "header"
      "main"
      "sidebar"
      "footer";
  }

  .featured {
    grid-column: span 1;
  }
}
```

This example demonstrates:

```text
.page
│
├── display: grid
├── Explicit rows and columns
├── Named grid areas
├── Responsive restructuring
│
├── .header
│   └── grid-area
│
├── .sidebar
│   ├── grid-area
│   └── Nested Grid
│
├── .main
│   └── .cards
│       ├── Nested Grid
│       ├── repeat()
│       ├── auto-fit
│       ├── minmax()
│       ├── fr
│       ├── gap
│       └── span
│
└── .footer
    └── grid-area
```

It also demonstrates an important principle of modern CSS:

> Layout systems can be nested and combined. A page can use Grid for its overall structure while individual components use Grid or Flexbox independently.

---

# **as) Key Takeaways**

CSS Grid is a **two-dimensional layout system** designed for controlling rows and columns simultaneously.

The Grid container is created with:

```css
display: grid;
```

and its direct children become Grid items.

The structure of the Grid is commonly defined with:

```css
grid-template-columns
grid-template-rows
```

Flexible tracks can be created using:

```css
fr
```

Repeated tracks can be simplified with:

```css
repeat()
```

Flexible minimum and maximum track sizes can be defined with:

```css
minmax()
```

Responsive Grid patterns frequently combine:

```css
repeat(
  auto-fit,
  minmax(250px, 1fr)
)
```

Elements can be precisely positioned with:

```css
grid-column
grid-row
```

or organized semantically with:

```css
grid-template-areas
grid-area
```

Grid can automatically generate additional tracks when the explicit Grid is insufficient, creating an **implicit grid**.

Finally:

```text
Flexbox
→ Excellent for one-dimensional
  component layouts.

Grid
→ Excellent for two-dimensional
  layouts involving rows and columns.

Grid + Flexbox
→ Often the best solution for
  complete modern interfaces.
```

---

# **References**

- **MDN Web Docs — Basic concepts of grid layout.** Covers Grid containers, tracks, lines, cells, areas, gutters, `fr`, explicit and implicit grids, alignment, and placement.

- **CSS-Tricks — A Complete Guide to CSS Grid.** Comprehensive reference covering Grid terminology, container and item properties, special units, functions, and common patterns.

- **LenguajeCSS — Guía de Introducción a Grid.** Covers Grid terminology, `grid` and `inline-grid`, row and column definitions, `fr`, `repeat()`, `minmax()`, `auto-fill`, `auto-fit`, and gaps.

- **LenguajeCSS — Grid por áreas.** Covers named Grid areas and page-layout patterns using `grid-template-areas`.

- **web.dev — Learn CSS: Grid.** Explains Grid as a two-dimensional layout system and its use for flexible, responsive page layouts.

- **MDN Web Docs — Grid layout using line-based placement.** Covers numbered Grid lines and precise item placement using row and column lines.
