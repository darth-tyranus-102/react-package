# HTML Cheat Sheet --- Web Programming Exam

**Based on the uploaded Weeks 5--8 exercises and the React project
examples in Weeks 9--12.** HTML provides the document structure; CSS
controls appearance; JavaScript adds behaviour.

## 1. Minimal HTML page

``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Web App</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header><h1>Page title</h1></header>
  <main>
    <section>
      <h2>Section title</h2>
      <p>Page content goes here.</p>
    </section>
  </main>
  <footer>Footer content</footer>
  <script src="script.js" defer></script>
</body>
</html>
```

-   `<!DOCTYPE html>` enables modern HTML rendering.
-   `meta charset` supports standard text characters.
-   The viewport meta tag makes layouts work on mobile screens.
-   `link` loads an external stylesheet.
-   `script ... defer` downloads JavaScript and runs it after HTML
    parsing.
-   Keep page content inside meaningful semantic elements where
    possible.

## 2. Common structural elements

  -----------------------------------------------------------------------
  Element                             Typical purpose
  ----------------------------------- -----------------------------------
  `<header>`                          Page or section introduction

  `<nav>`                             Navigation links

  `<main>`                            Main content (normally one per
                                      page)

  `<section>`                         Thematically grouped content

  `<article>`                         Self-contained item, post, or card

  `<aside>`                           Related/secondary content

  `<footer>`                          Closing or contact information

  `<div>`                             Generic block container

  `<span>`                            Generic inline container

  `<h1>`--`<h6>`                      Hierarchical headings

  `<p>`                               Paragraph

  `<ul>`, `<ol>`, `<li>`              Unordered/ordered lists

  `<a href="...">`                    Link

  `<img src="..." alt="...">`         Image; always provide useful `alt`
                                      text
  -----------------------------------------------------------------------

Example list and link:

``` html
<h2>Hobbies</h2>
<ul>
  <li>Reading</li>
  <li>Photography</li>
</ul>
<a href="contact.html">Contact us</a>
```

## 3. Forms and inputs

Forms appear in search, task creation, and inventory-style exercises.

``` html
<form id="medicine-form">
  <label for="medicine-name">Medicine name</label>
  <input id="medicine-name" name="name" type="text"
         placeholder="Enter name" required>

  <label for="quantity">Quantity</label>
  <input id="quantity" name="quantity" type="number"
         min="0" step="1" required>

  <label for="price">Price</label>
  <input id="price" name="price" type="number"
         min="0" step="0.01" required>

  <button type="submit">Add item</button>
</form>
```

Useful input attributes:

-   `type="text"` --- text.
-   `type="number"` --- numeric input.
-   `type="radio"` --- choose one option from a group.
-   `type="checkbox"` --- independent on/off selection.
-   `name` --- field key used by forms and JavaScript.
-   `id` --- unique element identifier.
-   `value` --- current/default value.
-   `placeholder` --- hint, not a replacement for a label.
-   `required` --- browser checks that a value exists.
-   `min`, `max`, `step` --- constrain numeric input.
-   `checked` --- initially selected checkbox/radio.
-   `disabled` --- prevents interaction.

### Radio buttons

``` html
<fieldset>
  <legend>Choose a delivery method</legend>
  <label><input type="radio" name="delivery" value="standard" checked> Standard</label>
  <label><input type="radio" name="delivery" value="express"> Express</label>
</fieldset>
```

Radio inputs share the same `name` so the user can select only one. In
JavaScript, query the checked option:

``` js
const selected = document.querySelector('input[name="delivery"]:checked');
console.log(selected ? selected.value : "No option selected");
```

### Accessible label rule

The label's `for` value should match the input's `id`:

``` html
<label for="search">Search employees</label>
<input id="search" type="text">
```

## 4. Tables

Useful for inventory and order lists.

``` html
<table>
  <thead>
    <tr><th>ID</th><th>Item</th><th>Quantity</th><th>Price</th></tr>
  </thead>
  <tbody id="inventory-body">
    <tr><td>1</td><td>Notebook</td><td>5</td><td>2.50</td></tr>
  </tbody>
</table>
```

Use `<th>` for headings, `<td>` for data cells, `<thead>` for column
headings, and `<tbody>` for records.

## 5. IDs, classes, and file linking

-   `id="search-box"` identifies one unique element.
-   `class="card"` can be reused on many elements.
-   CSS ID selector: `#search-box`.
-   CSS class selector: `.card`.
-   HTML tag selector: `button`.

Typical project structure:

``` text
my-project/
├── index.html
├── styles.css
└── script.js
```

Link files with relative paths:

``` html
<link rel="stylesheet" href="styles.css">
<script src="script.js" defer></script>
```

## 6. How HTML fits into a wider project

1.  Create semantic page structure in HTML.
2.  Add stable IDs/classes for styling and interaction.
3.  Put visual rules in CSS rather than inline styles when practical.
4.  Use JavaScript to read inputs, respond to events, and update the
    page.
5.  For React projects, HTML-like markup is written as **JSX** inside
    components rather than copied into a standalone HTML body.

Example integration: a search input is defined in HTML, styled using
`.search-input`, and read in JavaScript using
`document.querySelector('#search')`.

## Exam reminders

-   Close tags and nest elements correctly.
-   Use `class` in HTML, not `className` (React JSX uses `className`).
-   Use `for` on a normal HTML label; React JSX uses `htmlFor`.
-   Buttons inside forms default to submit; set `type="button"` for a
    non-submit action.
-   Do not use a placeholder as the only label.
