# CSS Exam-Solving Guide
**Web Programming | Page styling, layout, responsive design, and JavaScript-driven CSS**

## 1. Read the visual requirements as CSS tasks

| Question wording | CSS approach |
|---|---|
| Text colour/background | `color`, `background-color` |
| Space inside an element | `padding` |
| Space outside an element | `margin` |
| Rounded corners | `border-radius` |
| Border around a card | `border` |
| Put items in a row | `display: flex` |
| Stack items vertically | `flex-direction: column` |
| Center items along a flex axis | `justify-content: center` |
| Center across the cross-axis | `align-items: center` |
| Equal-width responsive columns | CSS Grid or flex wrapping |
| Keep footer at bottom on short pages | body flex column + `margin-top: auto` on footer |
| Change appearance on hover | `:hover` |
| Change layout on small screens | `@media` query |

## 2. The box model

Every element is a box: content, padding, border, and margin.

```css
* {
  box-sizing: border-box;
}

.card {
  width: 320px;
  padding: 20px;
  border: 1px solid #ccc;
  margin: 16px;
}
```

`box-sizing: border-box` makes declared width include content, padding, and border, which is easier for predictable layouts. Margin remains outside the border.

## 3. Selectors you must recognize

```css
p { color: #333; }            /* all p elements */
.card { padding: 1rem; }      /* any element with class="card" */
#main { max-width: 1100px; }  /* the element with id="main" */
header h1 { margin: 0; }      /* h1 descendants of header */
.card:hover { box-shadow: 0 4px 12px #0002; }
input[type="email"] { width: 100%; }
```

- `.class` selects all elements with a class.
- `#id` selects the element with that ID.
- `A B` selects descendants of `A`.
- `A > B` selects direct children only.
- `:hover` applies while the pointer is over the element.
- When styles seem ignored, check selector spelling, specificity, and whether the CSS file is linked.

## 4. Reusable page styling

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
  color: #222;
  background: #f5f7fa;
  line-height: 1.5;
}

.site-header,
.site-footer {
  padding: 1.5rem 2rem;
  background: #26364a;
  color: white;
}

main {
  width: min(100% - 2rem, 1100px);
  margin: 2rem auto;
}

.card {
  padding: 1.25rem;
  border: 1px solid #d9dee7;
  border-radius: 10px;
  background: white;
  box-shadow: 0 2px 8px #0000000d;
}

h1, h2, p {
  margin-top: 0;
}
```

For strict automated marking, follow the exact values and properties requested by the question; do not assume visually similar CSS will satisfy a property-specific test.

## 5. Flexbox: navbars, footers, rows, and centered content

```css
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.social-links {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.25rem;
}

.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.page footer {
  margin-top: auto;
}
```

Remember:
- `justify-content` controls distribution along the main axis.
- `align-items` controls alignment along the cross-axis.
- `flex-direction: column` changes the main axis from horizontal to vertical.
- `gap` creates space between flex/grid children without adding margins to each child.

## 6. Grid: responsive cards

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}
```

This lets cards fit as many columns as the available width allows. If a question specifically requires two columns, use an explicit two-column rule and add a media query if needed.

## 7. Forms and buttons

```css
form {
  display: grid;
  gap: 1rem;
  max-width: 520px;
}

input, select, textarea {
  width: 100%;
  padding: 0.7rem;
  border: 1px solid #aeb8c5;
  border-radius: 6px;
  font: inherit;
}

button {
  padding: 0.7rem 1rem;
  border: 0;
  border-radius: 6px;
  background: #1769aa;
  color: white;
  cursor: pointer;
}

button:hover {
  filter: brightness(0.9);
}
```

Do not remove focus indication without replacing it with a visible focus style.

## 8. Responsive design

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1rem;
}

@media (max-width: 700px) {
  .card-grid {
    grid-template-columns: 1fr;
  }

  .navbar {
    flex-direction: column;
    align-items: stretch;
  }
}
```

Use a media query when the question requires different styles at a specific viewport width. Check the exact breakpoint if one is stated.

## 9. Common task: style a footer with social icons

```css
footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem;
  background: #303e4f;
  color: white;
}

.social-media {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.social-media img {
  width: 24px;
  height: 24px;
}

.social-media a:hover {
  opacity: 0.75;
  transform: scale(1.08);
}
```

To keep the footer at the bottom when content is short, put the page in a flex column with `min-height: 100vh` and apply `margin-top: auto` to the footer.

## 10. JavaScript changes CSS

HTML:
```html
<p id="status">Waiting</p>
<button id="changeButton" type="button">Change style</button>
```

CSS:
```css
.highlight {
  color: #0b6b3a;
  font-weight: bold;
}
```

JavaScript:
```js
document.getElementById("changeButton").addEventListener("click", () => {
  document.getElementById("status").classList.toggle("highlight");
});
```

Prefer `classList.add`, `remove`, or `toggle` for reusable states. Use `element.style.property` for a direct one-off style change when the question specifically asks for it.

## 11. Debugging checklist

- Is the CSS file correctly linked?
- Is the selector targeting the correct element?
- Is the class name spelled the same in HTML and CSS?
- Is another rule overriding this rule?
- Is a property invalid or missing a unit (e.g. `margin: 10px`)?
- Is the layout using flex/grid on the parent, not only on the child?
- Does the media query condition match the current viewport?
- For strict marking, did you use the specifically requested properties and values?

## 12. Practice variations

1. Style a profile page with a dark header and light article panel.
2. Create a horizontal group of social icons and links.
3. Build responsive product cards.
4. Keep a footer at the bottom of a short page.
5. Style a form and show a clear hover/focus state.
6. Use JavaScript to add/remove a CSS class when a button is clicked.
