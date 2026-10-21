# React Exam-Solving Guide
**Web Programming | Weeks 8–12 patterns: components, props, state, search, filtering, timers, routing, reusable cards, and effects**

## 1. How to approach a React question

Before coding, identify:
1. What data exists? (employees, products, recipes, tasks, books, stops, cities)
2. Which parts should be reusable components?
3. What state changes after user interaction?
4. Which data is derived from existing data? (filtered list, total, converted temperature)
5. Which props does each child need?
6. Does the question require routing or an effect/timer?

A common structure is: **App owns data and state → passes props to child components → children render UI and report user actions through callbacks.**

## 2. Typical project structure

```text
src/
├── main.jsx
├── App.jsx
├── App.css
└── components/
    ├── EmployeeCard.jsx
    └── EmployeeCard.css
```

A component filename conventionally starts with a capital letter. Import paths and filenames must match exactly.

## 3. Components and JSX

```jsx
function EmployeeCard({ name, department, role }) {
  return (
    <article className="employee-card">
      <h2>{name}</h2>
      <p>{role}</p>
      <span>{department}</span>
    </article>
  );
}

export default EmployeeCard;
```

Use `className`, not `class`, in JSX. JavaScript expressions go inside `{}`. JSX must return one parent element (or a fragment `<>...</>`). List items should have stable `key` props.

Render it:
```jsx
<EmployeeCard
  name="Asha Patel"
  department="Engineering"
  role="Frontend Developer"
/>
```

## 4. Props versus state

- **Props** are inputs passed from a parent; a child should not mutate them.
- **State** is data managed by a component that can change over time.
- If multiple components need to update or share the same data, keep that state in their closest common parent and pass values/callbacks down.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Add</button>
    </div>
  );
}
```

Use `onClick={() => ...}` when passing a function that should run after the click. `onClick={setCount(count + 1)}` calls it during rendering and is a common mistake.

## 5. Render arrays and keys

```jsx
const employees = [
  { id: 1, name: "Asha", department: "Engineering" },
  { id: 2, name: "Ben", department: "Sales" }
];

function EmployeeList() {
  return (
    <div>
      {employees.map(employee => (
        <EmployeeCard
          key={employee.id}
          name={employee.name}
          department={employee.department}
          role="Team member"
        />
      ))}
    </div>
  );
}
```

Use a stable unique ID for `key`, not a random value generated during each render.

## 6. Search and filter patterns

This matches the employee directory, department filter, recipe finder, and similar course exercises.

```jsx
import { useState } from "react";

function EmployeeDirectory({ employees }) {
  const [query, setQuery] = useState("");
  const [department, setDepartment] = useState("All");

  const visibleEmployees = employees.filter(employee => {
    const matchesName = employee.name
      .toLowerCase()
      .includes(query.trim().toLowerCase());

    const matchesDepartment =
      department === "All" || employee.department === department;

    return matchesName && matchesDepartment;
  });

  return (
    <section>
      <input
        value={query}
        onChange={event => setQuery(event.target.value)}
        placeholder="Search employees"
      />

      <select
        value={department}
        onChange={event => setDepartment(event.target.value)}
      >
        <option>All</option>
        <option>Engineering</option>
        <option>Sales</option>
      </select>

      {visibleEmployees.length === 0 ? (
        <p>No matching employees found.</p>
      ) : (
        visibleEmployees.map(employee => (
          <EmployeeCard
            key={employee.id}
            name={employee.name}
            department={employee.department}
            role={employee.role}
          />
        ))
      )}
    </section>
  );
}
```

Pattern:
- State holds the user's search/filter selection.
- `filter` derives the visible records.
- The original array is not modified.
- The UI handles the empty-result case.

Adapt the property names and filter conditions to the supplied data.

## 7. Forms: controlled inputs

```jsx
function TaskForm({ onAddTask }) {
  const [title, setTitle] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
    const cleanedTitle = title.trim();
    if (!cleanedTitle) return;

    onAddTask(cleanedTitle);
    setTitle("");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={title}
        onChange={event => setTitle(event.target.value)}
        placeholder="Task title"
      />
      <button type="submit">Add task</button>
    </form>
  );
}
```

A controlled input uses `value={state}` and `onChange` to update that state. `event.preventDefault()` prevents the browser from reloading the page during a React form submission.

## 8. Updating arrays immutably

For a task manager or inventory application, never mutate the existing state array with `push`, `splice`, or direct item assignment. Create a new array.

Add:
```jsx
setTasks(previous => [
  ...previous,
  { id: Date.now(), title: newTitle, completed: false }
]);
```

Delete:
```jsx
setTasks(previous => previous.filter(task => task.id !== taskId));
```

Toggle:
```jsx
setTasks(previous =>
  previous.map(task =>
    task.id === taskId
      ? { ...task, completed: !task.completed }
      : task
  )
);
```

Update quantity:
```jsx
setItems(previous =>
  previous.map(item =>
    item.id === itemId
      ? { ...item, quantity: item.quantity + 1 }
      : item
  )
);
```

The functional setter form (`previous => ...`) is useful when the new value depends on the previous state.

## 9. Calculated values: discounts and temperature conversion

Keep the source value in state and calculate the displayed value.

```jsx
const [celsius, setCelsius] = useState(20);
const fahrenheit = (celsius * 9) / 5 + 32;
```

```jsx
const [price, setPrice] = useState(100);
const [discountEnabled, setDiscountEnabled] = useState(false);
const displayedPrice = discountEnabled ? price * 0.9 : price;
```

Do not keep multiple pieces of state for values that can be calculated from existing state unless the task has a specific reason to do so. This avoids values becoming inconsistent.

## 10. Reusable cards and component CSS

```jsx
function PriceTag({ price, discountEnabled }) {
  const finalPrice = discountEnabled ? price * 0.9 : price;

  return (
    <div className="price-tag">
      {discountEnabled && <span className="badge">10% off</span>}
      <strong>£{finalPrice.toFixed(2)}</strong>
    </div>
  );
}

export default PriceTag;
```

```css
.price-tag {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.badge {
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  background: #d9f5e5;
  color: #14532d;
}
```

A reusable component should describe one repeated UI unit and receive the changing data through props.

## 11. `useEffect`: timers and side effects

Use `useEffect` for synchronizing with something outside normal rendering, such as a timer or browser API. Do not use it merely to calculate a value that can be derived during rendering.

```jsx
import { useEffect, useState } from "react";

function Stopwatch() {
  const [seconds, setSeconds] = useState(0);
  const [running, setRunning] = useState(false);

  useEffect(() => {
    if (!running) return;

    const timerId = setInterval(() => {
      setSeconds(previous => previous + 1);
    }, 1000);

    return () => clearInterval(timerId);
  }, [running]);

  return (
    <section>
      <p>{Math.floor(seconds / 60)}:{String(seconds % 60).padStart(2, "0")}</p>
      <button onClick={() => setRunning(true)}>Start</button>
      <button onClick={() => setRunning(false)}>Stop</button>
      <button onClick={() => { setRunning(false); setSeconds(0); }}>Reset</button>
    </section>
  );
}
```

The cleanup function clears the interval when the effect is re-run or the component is removed. This prevents duplicate or orphaned timers.

For lap tracking, append the current elapsed time to a lap array when the lap button is clicked.

## 12. Class components and lifecycle (if the question uses them)

Some course solutions may use class components. Recognize the pattern even if you prefer function components:

```jsx
class Example extends React.Component {
  state = { count: 0 };

  componentDidMount() {
    // Runs after the component is mounted.
  }

  componentWillUnmount() {
    // Clean up timers/listeners if they were created.
  }

  render() {
    return (
      <button onClick={() => this.setState({ count: this.state.count + 1 })}>
        {this.state.count}
      </button>
    );
  }
}
```

Use the component style the question or starter project requires. Do not rewrite a class-based starter into hooks if the assessment expects a class component.

## 13. Routing pattern

If the task requires pages such as Home and Marks, use the router package and the version/configuration supplied by the starter project.

A common React Router v6-style pattern:

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function Home() {
  return <h1>Student Dashboard</h1>;
}

function Marks() {
  return <h1>Marks</h1>;
}

export default function App() {
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

Router versions differ. Follow the imports and patterns already installed in the project, and do not add a second `BrowserRouter` if the app is already wrapped by one.

## 14. Common exam patterns from the weekly exercises

| Task pattern | Core implementation |
|---|---|
| Medical shop / food order / music store / bookstore | Render data records; calculate totals; update cart/order state as required |
| Employee directory | `map` to render cards, `filter` for name/department |
| Stopwatch with laps | elapsed-time state, interval effect, cleanup, lap array |
| Crop/task dashboard | state for records and status; update/filter records |
| Book card / price tag | reusable component, props, conditional display |
| Student dashboard | reusable navigation and routes |
| Recipe cards/favourites | list rendering, search/filter, favourite ID state |
| Metro departure board | reusable stop card and list of departures |
| Temperature toggle | store one unit/value and derive the other |
| Task board | form submission, add/toggle/delete with immutable state |
| Coffee menu | reusable menu item component and data-driven rendering |
| Recipe finder | controlled search field, filter data, empty-state display |

Use the actual question's field names, data, requirements, and project dependencies; these are patterns, not a replacement for the supplied specification.

## 15. Common React mistakes

- Using `class` instead of `className`.
- Calling a state setter immediately in an event prop.
- Mutating state arrays/objects directly.
- Forgetting a unique `key` in a rendered list.
- Using props as if the child can change them.
- Storing derived values in state unnecessarily.
- Forgetting `event.preventDefault()` in a form.
- Not cleaning up intervals/listeners in effects.
- Filtering the wrong property or comparing values with different types.
- Assuming a package or import exists without checking the starter project.

## 16. A reliable implementation checklist

1. Confirm required files and export/import names.
2. Define the data shape.
3. Build the smallest component that renders one item.
4. Render the list with `.map()` and stable keys.
5. Add state for each user-controlled value.
6. Add event handlers.
7. Derive search/filter/total values from state.
8. Add empty and validation states.
9. Add CSS/Bootstrap styling.
10. Test add, edit, delete, filter, reset, and boundary cases required by the prompt.

## 17. Practice by changing the requirements

Take one working solution and alter it:
- Add a second filter to an employee directory.
- Add sorting by price.
- Prevent adding an empty task.
- Add a delete button to each task.
- Keep favourite recipe IDs in state.
- Change the discount from a fixed 10% to a user-selected percentage.
- Add a Celsius/Fahrenheit toggle.
- Add an empty search message.
- Add a lap list and clear-laps button to the stopwatch.

If you can make these changes and explain why they work, you are better prepared for variants of the same question.
