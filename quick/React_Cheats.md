# React Cheat Sheet --- Web Programming Exam

**Based on the uploaded Weeks 8--12 React exercises:** inventory tables,
order forms, stopwatches, searchable directories, crop dashboards, task
managers, reusable cards, favourites, routing, and temperature
conversion.

## 1. Typical React project structure

``` text
src/
├── index.js            # application entry point
├── App.js              # top-level composition
├── App.css             # global/page styles
└── components/
    ├── BookCard.jsx
    ├── BookCard.css
    ├── TaskForm.jsx
    └── TaskList.jsx
```

A common entry point (Create React App style):

``` jsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';

createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

Some older course examples use `ReactDOM.render`; newer React projects
use `createRoot`. Follow the version and starter files provided by the
exam environment.

## 2. Functional component and JSX

``` jsx
function BookCard() {
  return (
    <article className="book-card">
      <h2>The Alchemist</h2>
      <p>Author: Paulo Coelho</p>
    </article>
  );
}

export default BookCard;
```

JSX reminders: - Return one parent element (or a fragment `<>...</>`). -
Use `className`, not `class`. - Use `htmlFor`, not `for`, on labels. -
JavaScript expressions go inside `{ ... }`. - Inline style is an object:
`style={{ color: 'blue', marginTop: 12 }}`. - Component names start with
a capital letter.

## 3. Props: pass data into reusable components

``` jsx
function BookCard({ bookTitle, authorName, availabilityStatus }) {
  return (
    <div className="book-card">
      <h2>{bookTitle}</h2>
      <p>Author: {authorName}</p>
      <p>Status: {availabilityStatus}</p>
    </div>
  );
}

// Parent:
<BookCard
  bookTitle="The Alchemist"
  authorName="Paulo Coelho"
  availabilityStatus="Available"
/>
```

Props flow from parent to child. Do not mutate props inside the child.

### PropTypes (used in Week 11 examples)

``` jsx
import PropTypes from 'prop-types';

BookCard.propTypes = {
  bookTitle: PropTypes.string.isRequired,
  authorName: PropTypes.string.isRequired,
  availabilityStatus: PropTypes.string.isRequired,
};
```

Install/use `prop-types` only if the project has it available.

## 4. State with `useState`

Use state for values that change and should trigger a render.

``` jsx
import { useState } from 'react';

function DiscountPrice({ originalPrice }) {
  const [discounted, setDiscounted] = useState(false);
  const price = discounted ? originalPrice * 0.9 : originalPrice;

  return (
    <div>
      <p>Price: ₹{price.toFixed(2)}</p>
      <button onClick={() => setDiscounted((prev) => !prev)}>
        {discounted ? 'Remove Discount' : 'Apply Discount'}
      </button>
    </div>
  );
}
```

General pattern:

``` jsx
const [value, setValue] = useState(initialValue);
setValue(newValue);
```

Use functional updates when the next value depends on the previous
value:

``` jsx
setCount((previous) => previous + 1);
```

## 5. Controlled forms and adding inventory items

``` jsx
import { useState } from 'react';

function InventoryForm({ onAdd }) {
  const [name, setName] = useState('');
  const [quantity, setQuantity] = useState('');
  const [price, setPrice] = useState('');

  function handleSubmit(event) {
    event.preventDefault();
    if (!name.trim() || quantity === '' || price === '') return;

    onAdd({
      name: name.trim(),
      quantity: Number(quantity),
      price: Number(price),
    });

    setName('');
    setQuantity('');
    setPrice('');
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)}
             placeholder="Item name" required />
      <input type="number" min="0" value={quantity}
             onChange={(e) => setQuantity(e.target.value)} required />
      <input type="number" min="0" step="0.01" value={price}
             onChange={(e) => setPrice(e.target.value)} required />
      <button type="submit">Add item</button>
    </form>
  );
}
```

-   A controlled input uses `value` plus `onChange`.
-   `event.preventDefault()` prevents the form reload.
-   Input values are strings; convert numeric fields with `Number`,
    `parseInt`, or `parseFloat`.
-   Reset state after a successful submission.
-   Use `=== ''` to check empty numeric inputs where zero is a valid
    value.

## 6. Arrays: add, remove, filter, and render

``` jsx
const [tasks, setTasks] = useState([]);

function addTask(task) {
  setTasks((previous) => [...previous, task]);
}

function removeTask(indexToRemove) {
  setTasks((previous) =>
    previous.filter((_, index) => index !== indexToRemove)
  );
}

const visibleEmployees = employees.filter((employee) =>
  employee.toLowerCase().includes(query.toLowerCase())
);

return (
  <ul>
    {visibleEmployees.map((employee) => (
      <li key={employee}>{employee}</li>
    ))}
  </ul>
);
```

-   Add immutably: `[...previous, newItem]`.
-   Remove immutably: `filter`.
-   Transform/render: `map`.
-   Include a stable unique `key` for every rendered list item; prefer
    an item ID over array index when possible.

## 7. Inventory data pattern

``` jsx
const [inventory, setInventory] = useState([
  { id: 1, name: 'Paracetamol', quantity: 50, price: 2.5 },
]);

const newId = inventory.length
  ? Math.max(...inventory.map((item) => item.id)) + 1
  : 1;

const newItem = {
  id: newId,
  name: 'Aspirin',
  quantity: 30,
  price: 3,
};

setInventory((previous) => [...previous, newItem]);
```

Render a table:

``` jsx
<tbody>
  {inventory.map((item) => (
    <tr key={item.id}>
      <td>{item.id}</td>
      <td>{item.name}</td>
      <td>{item.quantity}</td>
      <td>${item.price.toFixed(2)}</td>
    </tr>
  ))}
</tbody>
```

## 8. Search and filtering

``` jsx
const [query, setQuery] = useState('');

const filtered = employees.filter((employee) =>
  employee.name.toLowerCase().includes(query.toLowerCase())
);

return (
  <>
    <input
      value={query}
      onChange={(event) => setQuery(event.target.value)}
      placeholder="Search employees"
    />
    {filtered.length === 0
      ? <p>No employees found</p>
      : filtered.map((employee) => (
          <EmployeeCard key={employee.id} {...employee} />
        ))}
  </>
);
```

Department filter:

``` jsx
const filtered = selectedDepartment === 'All'
  ? employees
  : employees.filter((employee) =>
      employee.department === selectedDepartment
    );
```

## 9. `useEffect` and lifecycle work

``` jsx
import { useEffect, useState } from 'react';

useEffect(() => {
  console.log('Component mounted or dependency changed');
}, [query]); // runs after render when query changes

useEffect(() => {
  const timerId = setInterval(() => {
    setTime((previous) => previous + 10);
  }, 10);

  return () => clearInterval(timerId); // cleanup
}, []);
```

-   `useEffect(fn, [])`: after initial mount; cleanup on unmount.
-   `useEffect(fn, [x])`: after mount and when `x` changes.
-   `useEffect(fn)`: after every render; use cautiously.
-   Always clean up intervals, subscriptions, or listeners when needed.

### Class component lifecycle (used in the course examples)

``` jsx
class Example extends React.Component {
  componentDidMount() {
    // setup after mounting
  }

  componentDidUpdate(prevProps, prevState) {
    // respond to changed props/state
  }

  componentWillUnmount() {
    // cleanup timers/listeners
  }

  render() {
    return <p>Hello</p>;
  }
}
```

Do not start a new interval on every update without checking state and
clearing the old interval.

## 10. Routing with React Router

The Week 11 dashboard uses `BrowserRouter`, `Routes`, `Route`, and
`Link`.

``` jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/marks">Marks</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/marks" element={<Marks />} />
      </Routes>
    </BrowserRouter>
  );
}
```

Use the package/version already configured in the project. A deployed
single-page app may need the host configured to serve `index.html` for
client-side routes.

## 11. React + CSS / Bootstrap

``` jsx
import './BookCard.css';

function BookCard() {
  return <div className="book-card"><h2>Book title</h2></div>;
}
```

Bootstrap example:

``` jsx
<div className="container my-4">
  <h1 className="text-primary mb-4">Inventory</h1>
  <table className="table table-striped table-bordered">
    {/* table rows */}
  </table>
  <button className="btn btn-success w-100">Add item</button>
</div>
```

If Bootstrap CSS is not already loaded, import it once in the app
entry/component:

``` jsx
import 'bootstrap/dist/css/bootstrap.min.css';
```

## 12. Project implementation checklist

1.  Read the question and identify data fields, controls, and expected
    visible text.
2.  Build a small reusable component for repeated UI (BookCard,
    StopCard, CityCard, MenuItem).
3.  Pass variable data as props.
4.  Store changing values in state.
5.  Implement handlers for submit, toggle, delete, filter, and search.
6.  Render arrays with `map` and stable keys.
7.  Validate blank inputs and convert number strings.
8.  Add CSS/Bootstrap classes matching the specification.
9.  Check empty states, disabled buttons, formatting, and exact labels.
10. Export each component and import it using the correct relative path.

## Exam pitfalls

-   JSX uses `className` and `htmlFor`.
-   Event handler is `onClick={handleClick}`, not
    `onClick={handleClick()}` unless intentionally invoking it.
-   Do not mutate state arrays with `push` or `splice`; create a new
    array.
-   Each mapped element needs a `key`.
-   Use `onChange` for controlled inputs.
-   Never call hooks inside loops, conditions, or nested functions.
-   Be careful with `0`: checking `!quantity` wrongly treats numeric
    zero as empty; check `quantity === ''` instead.
