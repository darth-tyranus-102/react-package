# Bootstrap Cheat Sheet --- Web Programming Exam

**Based on Bootstrap classes appearing in the uploaded React
solutions:** containers, spacing, typography, tables, forms, buttons,
grids, cards, badges, navigation, and loading indicators. Bootstrap is a
CSS framework; React still controls application data and behaviour.

## 1. Include Bootstrap

In a React component or entry file, if the project uses npm and
Bootstrap is installed:

``` jsx
import 'bootstrap/dist/css/bootstrap.min.css';
```

Or use the project's configured CDN stylesheet in the HTML `<head>`. Do
not include the same stylesheet repeatedly in many components.

## 2. Containers and spacing

``` jsx
<div className="container my-4">
  <h1 className="mb-4">Inventory</h1>
  <section className="p-4 mt-3">Content</section>
</div>
```

Common spacing utilities use `{property}{sides}-{size}`:

-   `m` = margin; `p` = padding.
-   `t`, `b`, `s`, `e`, `x`, `y` = top, bottom, start, end, horizontal,
    vertical.
-   Sizes commonly run from `0` to `5`; `auto` is available for some
    margin utilities.
-   Examples: `mt-3`, `mb-4`, `mx-auto`, `px-2`, `py-3`, `my-5`.

## 3. Typography and colours

``` jsx
<h1 className="text-primary">Page title</h1>
<h2 className="text-success mb-3">Add new item</h2>
<p className="text-muted">Helpful description</p>
<span className="text-danger">Error</span>
```

Common contextual colours include `primary`, `secondary`, `success`,
`danger`, `warning`, `info`, `light`, `dark`, and `muted` (for text).

Other useful classes: - `text-center`, `text-end` - `fw-bold`,
`fw-semibold` - `lead`, `small` - `text-decoration-line-through`

## 4. Buttons and widths

``` jsx
<button className="btn btn-success">Add</button>
<button className="btn btn-outline-primary">Filter</button>
<button className="btn btn-danger btn-sm">Delete</button>
<button className="btn btn-primary w-100">Full-width action</button>
```

-   `btn` is the base class; pair it with a variant.
-   `btn-sm` makes a smaller button.
-   `w-100` makes width 100%.
-   For a disabled button use the HTML/JSX `disabled` attribute, not
    just a colour class.

## 5. Tables

``` jsx
<table className="table table-striped table-bordered">
  <thead>
    <tr><th>ID</th><th>Name</th><th>Price</th></tr>
  </thead>
  <tbody>
    {items.map((item) => (
      <tr key={item.id}>
        <td>{item.id}</td>
        <td>{item.name}</td>
        <td>{item.price.toFixed(2)}</td>
      </tr>
    ))}
  </tbody>
</table>
```

Useful table classes: - `table` --- base table styling. -
`table-striped` --- alternating row background. - `table-bordered` ---
cell/table borders. - `table-hover` --- hover highlight. -
`table-warning`, `table-dark` --- contextual styling.

## 6. Forms and responsive grid

``` jsx
<form onSubmit={handleSubmit}>
  <div className="mb-3">
    <label htmlFor="item-name" className="form-label">Item name</label>
    <input
      id="item-name"
      className="form-control"
      value={name}
      onChange={(e) => setName(e.target.value)}
      required
    />
  </div>
  <button className="btn btn-success" type="submit">Add item</button>
</form>
```

-   `form-label` styles a label.
-   `form-control` styles text/number inputs and textareas.
-   `form-select` styles a select.
-   `form-check`, `form-check-input`, `form-check-label` are for
    checkbox/radio patterns.

Grid example:

``` jsx
<div className="row g-3">
  <div className="col-12 col-md-6 col-lg-4">Card A</div>
  <div className="col-12 col-md-6 col-lg-4">Card B</div>
  <div className="col-12 col-md-6 col-lg-4">Card C</div>
</div>
```

-   `.row` establishes a grid row.
-   `g-3` adds gutters/gaps.
-   `col-12` takes full width on extra-small screens.
-   `col-md-6` takes half width at medium screens and up.
-   `col-lg-4` takes one-third width at large screens and up.

## 7. Cards, badges, and alignment

``` jsx
<div className="card h-100 shadow-sm">
  <div className="card-body d-flex flex-column justify-content-between">
    <div>
      <h5 className="card-title">Book title</h5>
      <p className="card-text">Author name</p>
    </div>
    <span className="badge bg-info">Available</span>
  </div>
</div>
```

-   `card`, `card-body`, `card-title`, `card-text` are card primitives.
-   `shadow-sm` adds a subtle shadow.
-   `h-100` fills the parent height.
-   `d-flex`, `flex-column`, `justify-content-between`,
    `align-items-center` are flex utilities.
-   `badge bg-info`, `badge bg-warning text-dark` style status labels.

## 8. Navigation and loading indicators

``` jsx
<nav className="navbar navbar-expand-lg navbar-dark bg-dark mb-4">
  <div className="container">
    <span className="navbar-brand">Task Manager</span>
  </div>
</nav>
```

Spinner pattern:

``` jsx
<div className="d-flex justify-content-center my-5">
  <div className="spinner-border text-primary" role="status">
    <span className="visually-hidden">Loading...</span>
  </div>
</div>
```

## 9. Bootstrap in a wider React project

1.  Confirm Bootstrap is installed or loaded by the starter project.
2.  Import Bootstrap CSS once.
3.  Use Bootstrap layout/utilities for the overall page and repeated UI.
4.  Keep custom CSS for requirements that Bootstrap does not cover.
5.  Use React state for behaviour (filters, form values, toggles);
    Bootstrap classes only control appearance.
6.  Check responsive layouts at small and large viewport widths.

## 10. Quick translation table

  --------------------------------------------------------------------------
  Need                                Bootstrap class
  ----------------------------------- --------------------------------------
  Centred page container              `container`

  Space below heading                 `mb-4`

  Primary heading                     `text-primary`

  Green add button                    `btn btn-success`

  Full-width button                   `w-100`

  Striped bordered table              `table table-striped table-bordered`

  Styled input                        `form-control`

  Styled select                       `form-select`

  Responsive 3-column card layout     `row g-3` + `col-12 col-md-6 col-lg-4`

  Card with shadow                    `card shadow-sm`

  Horizontal flex row                 `d-flex align-items-center`

  Space content to opposite ends      `justify-content-between`

  Small status label                  `badge bg-info`

  Strike through completed task       `text-decoration-line-through`
  --------------------------------------------------------------------------

## Exam pitfalls

-   In React JSX, write `className`, not `class`.
-   Bootstrap styling does not implement search/filter/add/delete logic;
    JavaScript or React must do that.
-   `form-control` is for inputs; `form-select` is for select elements.
-   Make sure the stylesheet is actually loaded before assuming a class
    has no effect.
-   Bootstrap versions differ; use classes supported by the version in
    the exam starter project.
