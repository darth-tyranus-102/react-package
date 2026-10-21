# JavaScript Cheat Sheet --- Web Programming Exam

**Based on the uploaded Weeks 6--8 DOM exercises and the logic used by
later React examples.** Plain JavaScript manipulates DOM elements; React
usually updates the interface through state.

## 1. Variables, strings, numbers, and templates

``` js
const employeeName = "Jane Smith"; // cannot reassign the binding
let quantity = 3;                  // can reassign
const price = 2.5;

const message = `${employeeName} has ${quantity} items`;
const total = quantity * price;
```

-   Use `const` by default and `let` when reassignment is required.
-   Input `.value` is usually a **string**, even for `type="number"`;
    convert it before arithmetic.
-   `Number(value)`, `parseInt(value, 10)`, and `parseFloat(value)`
    convert numeric strings.
-   `===` checks strict equality; prefer it over `==`.

## 2. DOM selection and content

``` js
const heading = document.querySelector('#title');
const cards = document.querySelectorAll('.card');

heading.textContent = 'Updated title';
heading.style.color = 'blue';
heading.classList.add('active');
heading.classList.remove('active');
heading.classList.toggle('active');
```

-   `querySelector` returns the first matching element.
-   `querySelectorAll` returns all matching elements.
-   `textContent` sets plain text safely.
-   `innerHTML` parses HTML markup; only use it with
    trusted/appropriately escaped content.
-   `classList` is often the best way to switch styles.

## 3. Event listeners

``` html
<input id="search" type="text" placeholder="Search employees">
<p id="result"></p>
```

``` js
const search = document.querySelector('#search');
const result = document.querySelector('#result');

search.addEventListener('input', (event) => {
  result.textContent = `Searching for: ${event.target.value}`;
});
```

Common events: - `click` --- user clicks. - `input` --- field value
changes as the user types. - `change` --- committed change, often
select/radio/checkbox. - `submit` --- form submission. -
`DOMContentLoaded` --- HTML has been parsed.

If the script is in the `<head>`, use `defer` or wait for
`DOMContentLoaded`.

## 4. Forms, validation, and preventing page reload

``` html
<form id="task-form">
  <input id="task-text" required placeholder="Enter a task">
  <button type="submit">Add task</button>
</form>
<ul id="task-list"></ul>
```

``` js
const form = document.querySelector('#task-form');
const input = document.querySelector('#task-text');
const list = document.querySelector('#task-list');

form.addEventListener('submit', (event) => {
  event.preventDefault();

  const task = input.value.trim();
  if (task === '') return;

  const li = document.createElement('li');
  li.textContent = task;
  list.appendChild(li);
  input.value = '';
});
```

-   `event.preventDefault()` stops the browser's default form
    navigation/reload.
-   `.trim()` removes leading/trailing whitespace.
-   Validate empty values before updating the page.
-   `createElement` plus `textContent` avoids treating user input as
    HTML.

## 5. Conditions and loops

``` js
if (quantity > 0) {
  console.log('In stock');
} else {
  console.log('Out of stock');
}

for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

Array iteration:

``` js
const names = ['John', 'Jane', 'Mike'];
names.forEach((name) => console.log(name));
```

## 6. Array methods used in the exercises

``` js
const employees = ['John Doe', 'Jane Smith', 'Mike Johnson'];

const filtered = employees.filter((name) =>
  name.toLowerCase().includes('ja')
);

const upperNames = employees.map((name) => name.toUpperCase());
const nextId = Math.max(...[1, 2, 3]) + 1;
```

-   `filter` returns a new array containing items that pass a condition.
-   `map` returns a new array by transforming every item.
-   `includes` checks whether a string/array contains a value.
-   `toLowerCase()` enables case-insensitive text matching.
-   `Math.max(...array)` spreads array values into function arguments;
    handle an empty array separately.

## 7. Radio buttons and checkboxes

``` js
const choice = document.querySelector('input[name="plan"]:checked');
const chosenPlan = choice ? choice.value : null;

const checkbox = document.querySelector('#terms');
if (checkbox.checked) {
  console.log('Terms accepted');
}
```

For radio buttons, same-name inputs form one group. For checkboxes, read
`.checked`.

## 8. Timers: stopwatch pattern

``` js
let elapsed = 0;
let intervalId = null;

function start() {
  if (intervalId !== null) return; // prevent multiple intervals
  intervalId = setInterval(() => {
    elapsed += 10;
    console.log(elapsed);
  }, 10);
}

function stop() {
  clearInterval(intervalId);
  intervalId = null;
}

function reset() {
  stop();
  elapsed = 0;
}
```

-   `setInterval(callback, milliseconds)` repeats a callback.
-   `clearInterval(id)` stops it.
-   Keep the timer ID so you can stop it.
-   Real elapsed time should ideally be calculated from timestamps
    rather than assuming each callback fires exactly on time.
-   In React, clean up intervals when the component unmounts.

## 9. Format time and currency

``` js
function formatTime(ms) {
  const minutes = Math.floor(ms / 60000);
  const seconds = Math.floor((ms % 60000) / 1000);
  const centiseconds = Math.floor((ms % 1000) / 10);
  const pad = (n) => String(n).padStart(2, '0');
  return `${pad(minutes)}:${pad(seconds)}.${pad(centiseconds)}`;
}

const price = 2.5;
console.log(price.toFixed(2)); // "2.50"
```

`toFixed(2)` returns a string formatted to two decimal places.

## 10. How JavaScript fits into a wider project

For a plain HTML/CSS/JS project: 1. Add controls and output containers
in HTML. 2. Style them in CSS. 3. Select elements and register listeners
in JS. 4. Validate input, calculate results, and update the DOM. 5.
Separate code into files such as `index.html`, `styles.css`, and
`script.js`.

For React, put interactive data in state and render from that state
instead of manually editing DOM nodes. Use React state for tasks,
filters, inventory, and unit toggles.

## Exam pitfalls

-   `.value` is a string; convert it before math.
-   Use `===`, not accidental assignment `=`, in comparisons.
-   `filter` returns a new array; it does not mutate the original array.
-   Prevent default form submission if the page should not reload.
-   Do not create a new timer interval every render/event without
    clearing the previous one.
