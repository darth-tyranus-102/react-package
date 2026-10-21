# CSS Cheat Sheet --- Web Programming Exam

**Based on the uploaded profile pages, cards, forms, tables, stopwatch,
and interactive projects.**

## 1. Add CSS to a project

External CSS is the usual pattern:

``` html
<link rel="stylesheet" href="styles.css">
```

``` css
/* styles.css */
body {
  margin: 0;
  font-family: Arial, sans-serif;
  color: #222;
  background-color: #f3f4f6;
}
```

In React, import the stylesheet in the component:

``` jsx
import './BookCard.css';
```

## 2. Selectors

``` css
/* Tag selector */
body { margin: 0; }

/* Class selector: reusable */
.card { padding: 1rem; }

/* ID selector: unique element */
#page-title { text-align: center; }

/* Descendant selector */
.card h2 { margin-top: 0; }

/* Multiple selectors share rules */
h1, h2 { line-height: 1.2; }

/* State selector */
button:hover { opacity: 0.85; }

/* Attribute selector */
input[type="number"] { max-width: 10rem; }
```

HTML example:

``` html
<div class="card">
  <h2 id="page-title">Inventory</h2>
</div>
```

## 3. The box model

Every element consists of content, padding, border, and margin.

``` css
* {
  box-sizing: border-box;
}

.card {
  width: 100%;
  max-width: 400px;
  padding: 24px;
  border: 2px solid #6c63ff;
  margin: 24px auto;
  border-radius: 10px;
}
```

-   `padding`: space inside the border.
-   `border`: line around the padding/content.
-   `margin`: space outside the border.
-   `box-sizing: border-box`: width includes padding and border.
-   `margin: 24px auto`: vertical margin plus horizontal centring for a
    block with a constrained width.

## 4. Common properties

  -----------------------------------------------------------------------------------
  Property                Example                             What it does
  ----------------------- ----------------------------------- -----------------------
  `color`                 `color: #333;`                      Text colour

  `background-color`      `background-color: white;`          Background

  `font-family`           `font-family: Arial, sans-serif;`   Typeface

  `font-size`             `font-size: 1.2rem;`                Text size

  `font-weight`           `font-weight: bold;`                Text thickness

  `text-align`            `text-align: center;`               Horizontal text
                                                              alignment

  `margin`                `margin: 1rem auto;`                Outer spacing

  `padding`               `padding: 1rem;`                    Inner spacing

  `border`                `border: 1px solid #ccc;`           Border

  `border-radius`         `border-radius: 8px;`               Rounded corners

  `box-shadow`            `box-shadow: 0 4px 12px #0002;`     Shadow

  `width` / `max-width`   `max-width: 600px;`                 Element width
                                                              constraints

  `display`               `display: flex;`                    Layout mode

  `gap`                   `gap: 1rem;`                        Space between flex/grid
                                                              items

  `overflow-y`            `overflow-y: auto;`                 Vertical scrolling if
                                                              needed
  -----------------------------------------------------------------------------------

## 5. Flexbox layouts

Useful for navigation bars, stop cards, buttons, and alignment.

``` css
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.button-row {
  display: flex;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}
```

-   `display: flex` creates a flex container.
-   `justify-content` aligns items along the main axis.
-   `align-items` aligns items across the cross axis.
-   `flex-direction: column` stacks items vertically.
-   `flex-wrap: wrap` lets items move onto another line.
-   `gap` adds space between items.

## 6. Grid and responsive layouts

``` css
.employee-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}
```

A media query applies rules at a viewport width:

``` css
@media (max-width: 600px) {
  .navbar {
    flex-direction: column;
    align-items: stretch;
  }

  .card {
    margin: 12px;
    padding: 16px;
  }
}
```

## 7. Reusable card pattern

``` css
.book-card {
  background: #fff;
  border: 2px solid #6c63ff;
  border-radius: 10px;
  padding: 24px;
  max-width: 400px;
  margin: 20px auto;
  text-align: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.book-card h2 {
  color: #6c63ff;
  margin-bottom: 12px;
}

.book-card .status {
  color: #27ae60;
  font-weight: bold;
}
```

``` html
<div class="book-card">
  <h2>The Alchemist</h2>
  <p>Author: Paulo Coelho</p>
  <p class="status">Available</p>
</div>
```

## 8. Styling forms and buttons

``` css
input, select {
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  font: inherit;
}

button {
  border: 0;
  border-radius: 6px;
  padding: 10px 18px;
  background: #2563eb;
  color: white;
  cursor: pointer;
}

button:hover { background: #1d4ed8; }
button:disabled { opacity: 0.5; cursor: not-allowed; }
```

## 9. CSS controlled by JavaScript

JavaScript can add/remove a class:

``` css
.highlight { background-color: #fff3b0; }
```

``` js
document.querySelector('#message').classList.toggle('highlight');
```

This is often cleaner than setting many inline styles in JavaScript.

## 10. How CSS fits into a wider project

-   Keep global styles (body, typography, page background) in `App.css`
    or `styles.css`.
-   Keep component-specific rules in files such as `BookCard.css` or
    `StopCard.css`.
-   Use classes for reusable styling; reserve IDs for unique elements or
    when a specification explicitly requires an ID.
-   Prefer responsive widths (`width: 100%`, `max-width`) over fixed
    page widths.
-   Use Bootstrap classes when the project already uses Bootstrap; avoid
    fighting the framework with unnecessary overrides.

## Exam pitfalls

-   CSS class selector starts with `.`, ID selector starts with `#`.
-   A missing semicolon may cause confusing parsing issues; include
    semicolons consistently.
-   `justify-content` and `align-items` need a flex/grid layout to have
    their intended effect.
-   `margin` is outside; `padding` is inside.
-   Check exact class/ID names when unit tests expect specific
    selectors.
