# Bootstrap Exam-Solving Guide
**Web Programming | Bootstrap utilities, grid, forms, buttons, cards, tables, and React integration**

## 1. What Bootstrap does

Bootstrap is a CSS framework with prebuilt layout rules, components, and utility classes. It does not replace HTML or JavaScript; it reduces the amount of custom CSS needed for common layouts and UI elements.

In a question, identify whether you need:
- **Layout:** `.container`, `.row`, `.col-*`
- **Spacing:** `m-*`, `p-*`, `mt-*`, `mb-*`, `gap-*`
- **Text/colour:** `text-*`, `bg-*`
- **Controls:** `.btn`, `.form-control`, `.form-select`
- **Content blocks:** `.card`, `.badge`, `.table`
- **Responsive behaviour:** breakpoint classes such as `col-md-6`

## 2. Include Bootstrap

Use the exact version and import method required by the starter project. A common CDN setup is:

```html
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
  rel="stylesheet"
>
```

If the project already imports Bootstrap through a package or stylesheet, do not add a duplicate import without a reason. For React projects, follow the supplied setup.

## 3. Containers and grid

```html
<div class="container py-4">
  <div class="row g-3">
    <div class="col-12 col-md-6 col-lg-4">
      <div class="card h-100">
        <div class="card-body">
          <h2 class="h5 card-title">Card one</h2>
          <p class="card-text">Description.</p>
        </div>
      </div>
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <div class="card h-100">
        <div class="card-body">Card two</div>
      </div>
    </div>
  </div>
</div>
```

Interpretation:
- `container` centers and constrains content at standard breakpoints.
- `row` creates a grid row.
- `col-12` makes a column full-width on small screens.
- `col-md-6` makes it half-width from the medium breakpoint.
- `col-lg-4` makes it one-third width from the large breakpoint.
- `g-3` controls row/column gutters.
- `h-100` stretches cards to full available height in their row.

The grid is based on 12 columns: `col-6` is half, `col-4` is one-third, `col-3` is one-quarter.

## 4. Spacing and alignment utilities

| Class | Meaning |
|---|---|
| `m-3` | Margin on all sides |
| `mt-3` | Margin top |
| `mb-4` | Margin bottom |
| `p-3` | Padding on all sides |
| `px-4` | Horizontal padding |
| `py-2` | Vertical padding |
| `d-flex` | Flex display |
| `justify-content-between` | Space items along main axis |
| `align-items-center` | Align items on cross-axis |
| `gap-2` | Gap between flex/grid items |
| `text-center` | Center text |
| `w-100` | Width 100% |
| `h-100` | Height 100% |
| `d-none` | Hide element |
| `d-md-block` | Display as block from medium breakpoint |

Bootstrap spacing numbers use a framework scale; do not assume `p-3` means 3 pixels.

## 5. Buttons, forms, and tables

```html
<button class="btn btn-primary" type="button">Save</button>
<button class="btn btn-outline-secondary" type="button">Cancel</button>

<div class="mb-3">
  <label for="email" class="form-label">Email</label>
  <input id="email" class="form-control" type="email" required>
</div>

<div class="mb-3">
  <label for="department" class="form-label">Department</label>
  <select id="department" class="form-select">
    <option>All</option>
    <option>Engineering</option>
  </select>
</div>

<table class="table table-striped table-hover">
  <thead>
    <tr><th scope="col">Name</th><th scope="col">Department</th></tr>
  </thead>
  <tbody>
    <tr><td>Asha</td><td>Engineering</td></tr>
  </tbody>
</table>
```

Useful button variants include `btn-primary`, `btn-secondary`, `btn-success`, `btn-danger`, `btn-warning`, and outline variants. Choose the variant required by the question.

## 6. Cards and badges

```html
<div class="card shadow-sm">
  <div class="card-body">
    <div class="d-flex justify-content-between align-items-start">
      <h2 class="card-title h5">Notebook</h2>
      <span class="badge text-bg-success">In stock</span>
    </div>
    <p class="card-text">A ruled notebook.</p>
    <p class="fw-bold mb-3">£3.50</p>
    <button class="btn btn-primary">Add to basket</button>
  </div>
</div>
```

In React, JSX uses `className` instead of `class`.

## 7. Bootstrap with React

```jsx
function ProductCard({ product, onAdd }) {
  return (
    <div className="card h-100">
      <div className="card-body d-flex flex-column">
        <h2 className="card-title h5">{product.name}</h2>
        <p className="card-text">{product.description}</p>
        <strong className="mb-3">£{product.price.toFixed(2)}</strong>
        <button
          className="btn btn-primary mt-auto"
          onClick={() => onAdd(product.id)}
        >
          Add to basket
        </button>
      </div>
    </div>
  );
}
```

Bootstrap handles presentation; React handles data, rendering, and state. The `onAdd` callback is passed by the parent component.

## 8. Combine Bootstrap with custom CSS

Use Bootstrap utilities first for standard spacing, colours, alignment, and grid. Add custom CSS for design details that utilities do not express clearly.

```jsx
<div className="card product-card shadow-sm">
  ...
</div>
```

```css
.product-card {
  border-radius: 0.75rem;
  transition: transform 0.2s ease;
}

.product-card:hover {
  transform: translateY(-3px);
}
```

Avoid adding many contradictory utility classes and custom rules to the same element. When a style seems ineffective, inspect which rule wins.

## 9. Responsive layout patterns

Three cards across large screens, two on medium, one on small:
```html
<div class="row g-3">
  <div class="col-12 col-md-6 col-lg-4">...</div>
  <div class="col-12 col-md-6 col-lg-4">...</div>
  <div class="col-12 col-md-6 col-lg-4">...</div>
</div>
```

A responsive navbar can use Bootstrap's navbar components, but a collapsing navbar also requires the appropriate Bootstrap JavaScript bundle and correct attributes. If the question only needs a simple static navigation bar, do not add unnecessary complexity.

## 10. Common mistakes

- Forgetting to import Bootstrap or using a mismatched version.
- Using `class` in JSX instead of `className`.
- Putting `.col-*` directly in a layout without a `.row` when using the standard grid pattern.
- Assuming spacing class numbers are pixel values.
- Using the wrong breakpoint class.
- Expecting interactive Bootstrap components to work without the required JavaScript.
- Adding a second Bootstrap import when the starter project already imports it.
- Writing custom CSS that unintentionally overrides Bootstrap.

## 11. Exam strategy

1. Build the correct HTML/React structure first.
2. Use Bootstrap grid classes for layout.
3. Add utilities for spacing, alignment, and text.
4. Add the required component classes.
5. Add custom CSS only for remaining visual requirements.
6. Check responsive behaviour and verify all class names.

## 12. Practice variations

1. Build a responsive product-card grid.
2. Create a striped table with hover styling.
3. Style a form with labels, input controls, and a submit button.
4. Make a card use `h-100` and a button align to the bottom.
5. Render a list of React records as Bootstrap cards.
6. Add a badge that changes according to stock or task status.
