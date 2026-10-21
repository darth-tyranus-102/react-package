# Web Programming Exam Study Map
**Use this file first. The five subject guides are designed to be searched independently.**

## Which guide should I open?

| If the question asks you to… | Start with |
|---|---|
| Structure a profile, event, form, list, table, or footer | `HTML_Exam_Guide.md` |
| Style a page, create a layout, use flex/grid, or respond to screen size | `CSS_Exam_Guide.md` |
| React to clicks, validate input, use loops/radio buttons, update the DOM, or run a timer | `JavaScript_Exam_Guide.md` |
| Build reusable components, pass props, manage state, search/filter records, manage tasks/favourites, or route between pages | `React_Exam_Guide.md` |
| Use Bootstrap grid, cards, buttons, forms, tables, spacing utilities, or responsive classes | `Bootstrap_Exam_Guide.md` |

## Topic map based on the uploaded Weeks 5–12 solution collection

The uploaded solution collection covers these broad patterns:
- **Week 5:** HTML page structure and CSS styling for profiles, event content, lists, and footers.
- **Week 6:** HTML/CSS page building and correcting code.
- **Week 7:** loops, external JavaScript, and radio-button interactions.
- **Week 8:** manipulating CSS with JavaScript and React exercises including an employee directory and stopwatch.
- **Week 9:** React data-driven examples for medical shop, food ordering, music store, and bookstore.
- **Week 10:** employee search, stopwatch with lap tracking, crop dashboard, and task manager.
- **Week 11:** reusable book card, price/discount component, student dashboard routing, employee filtering, and recipe favourites.
- **Week 12:** metro departure board, temperature-unit toggle, task board, coffee menu, and recipe finder.

The guides below expand the reusable concepts needed to solve related variations. They do not imply that every variation is guaranteed to appear in the exam. Follow the exact requirements and starter files given in the question.

## A repeatable method for coding questions

1. **Extract requirements.** List the required UI elements, inputs, data, actions, and output.
2. **Identify the layer.** HTML = structure; CSS/Bootstrap = presentation; JavaScript/React = behaviour and state.
3. **Choose a pattern.** Form, card, list rendering, filter, timer, route, or calculation.
4. **Write the smallest working solution.** Do not start with optional styling.
5. **Check names.** IDs, classes, props, component names, file paths, and data keys must match.
6. **Handle edge cases.** Empty input, no search matches, invalid numbers, no radio selection, zero items, repeated clicks.
7. **Test each action.** Submit, search, filter, add, remove, toggle, start, stop, reset, and route as applicable.
8. **Match the specification.** Automated marking may require exact file names, exports, property names, or CSS values.

## How to study from the guides tonight

For each topic:
1. Read the pattern and explanation.
2. Hide the solution and reproduce it.
3. Change at least one requirement.
4. Explain aloud why each important line is there.
5. Test one normal case and one edge case.

Prioritize JavaScript and React practice if the question style involves multiple interacting requirements, state updates, filtering, or event handling. Still check the exact emphasis in your own uploaded questions before choosing what to skip.

## Quick reference: the core patterns

### HTML
```html
<form id="form">
  <label for="name">Name</label>
  <input id="name" name="name" required>
  <button type="submit">Submit</button>
</form>
```

### CSS
```css
* { box-sizing: border-box; }
.layout { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1rem; }
```

### JavaScript
```js
form.addEventListener("submit", event => {
  event.preventDefault();
  // read → validate → calculate → display
});
```

### React
```jsx
const [items, setItems] = useState([]);
setItems(previous => [...previous, newItem]);
```

### Bootstrap
```html
<div class="container py-4">
  <div class="row g-3">
    <div class="col-12 col-md-6 col-lg-4">
      <div class="card h-100"><div class="card-body">Content</div></div>
    </div>
  </div>
</div>
```
