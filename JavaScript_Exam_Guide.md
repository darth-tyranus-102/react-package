# JavaScript Exam-Solving Guide
**Web Programming | Events, loops, radio buttons, DOM updates, validation, and CSS manipulation**

## 1. A reliable approach to any JavaScript question

Translate the prompt into this sequence:

1. **Select** the HTML elements you need.
2. **Read** input values or the current state.
3. **Convert** values to the correct type.
4. **Check** the requirements using `if` statements.
5. **Calculate or transform** the data.
6. **Update** the page or CSS.
7. **Test** empty input, invalid values, and boundary cases.

Most beginner tasks are a combination of these steps.

## 2. Variables, values, and conversions

```js
const name = "Sam";           // string
const quantity = Number("4"); // number 4
let total = 0;                // reassignment is allowed
const isValid = true;         // boolean
```

- Use `const` when the variable will not be reassigned.
- Use `let` when reassignment is required.
- `input.value` is normally a string, even for a number input.
- Convert before arithmetic: `const price = Number(priceInput.value)`.
- Check numeric validity with `Number.isFinite(value)` or `Number.isNaN(value)`.

## 3. Selecting and changing the DOM

```js
const heading = document.getElementById("heading");
const message = document.querySelector(".message");

heading.textContent = "Updated heading";
message.textContent = "Operation complete";
```

Useful selectors:
```js
document.getElementById("result");
document.querySelector("#result");
document.querySelector(".card");
document.querySelectorAll(".item");
```

Use `textContent` for plain text. `innerHTML` parses HTML and should not be filled with untrusted user input.

## 4. Events: the standard pattern

```html
<button id="runButton" type="button">Run</button>
<p id="result"></p>
```

```js
const button = document.getElementById("runButton");
const result = document.getElementById("result");

button.addEventListener("click", () => {
  result.textContent = "Button clicked";
});
```

Do not call the handler immediately by writing `addEventListener("click", handler())`; pass the function itself or use a callback.

For a form, use the `submit` event and prevent a full page reload when handling it with JavaScript:

```js
document.getElementById("myForm").addEventListener("submit", (event) => {
  event.preventDefault();
  // Read inputs, validate, and update the page here.
});
```

## 5. Form validation: full worked pattern

```html
<form id="priceForm">
  <label for="quantity">Quantity</label>
  <input id="quantity" type="number" min="1" required>

  <label for="unitPrice">Unit price</label>
  <input id="unitPrice" type="number" min="0" step="0.01" required>

  <button type="submit">Calculate</button>
</form>
<p id="output" aria-live="polite"></p>
```

```js
const form = document.getElementById("priceForm");
const output = document.getElementById("output");

form.addEventListener("submit", (event) => {
  event.preventDefault();

  const quantity = Number(document.getElementById("quantity").value);
  const unitPrice = Number(document.getElementById("unitPrice").value);

  if (!Number.isFinite(quantity) || quantity < 1 ||
      !Number.isFinite(unitPrice) || unitPrice < 0) {
    output.textContent = "Enter a valid quantity and price.";
    return;
  }

  const total = quantity * unitPrice;
  output.textContent = `Total: £${total.toFixed(2)}`;
});
```

Why this works:
- Reads values only after submission.
- Converts strings to numbers.
- Rejects invalid values before calculation.
- Uses `return` to stop invalid processing.
- Updates a known output element.
- Formats the result to two decimal places.

Adapt the calculation and validation conditions to the actual question.

## 6. Radio buttons and checkboxes

Get the selected radio value:
```js
const selected = document.querySelector('input[name="payment"]:checked');

if (selected) {
  console.log(selected.value);
} else {
  console.log("Choose a payment method.");
}
```

Read a checkbox:
```js
const accepted = document.getElementById("terms").checked;
if (!accepted) {
  // Show a validation message.
}
```

The distinction is crucial: `.value` is the option's value; `.checked` tells you whether it is selected.

## 7. Conditions and loops

```js
if (score >= 70) {
  result = "Distinction";
} else if (score >= 50) {
  result = "Pass";
} else {
  result = "Retry";
}
```

```js
for (let i = 0; i < items.length; i++) {
  console.log(items[i]);
}
```

A `for` loop is useful when you need an index or exact iteration control. `for...of` is convenient for values:

```js
for (const item of items) {
  console.log(item);
}
```

Common errors:
- Using `=` instead of `===` for comparison.
- Forgetting to convert a numeric input.
- Using `i <= array.length`, which accesses one item past the end; normally use `i < array.length`.
- Forgetting braces around multiple statements.
- Not handling empty arrays or empty input.

## 8. Arrays: search, filter, and transform

```js
const products = [
  { id: 1, name: "Notebook", price: 3 },
  { id: 2, name: "Pen", price: 1 },
  { id: 3, name: "Bag", price: 20 }
];

const affordable = products.filter(product => product.price < 10);
const notebook = products.find(product => product.name === "Notebook");
const names = products.map(product => product.name);
```

- `map` creates a transformed array.
- `filter` keeps elements that pass a condition.
- `find` returns the first matching element or `undefined`.
- `forEach` runs a callback for each element but does not create a transformed result array.

For a case-insensitive search:
```js
const query = searchInput.value.trim().toLowerCase();
const matches = products.filter(product =>
  product.name.toLowerCase().includes(query)
);
```

## 9. Manipulating CSS with JavaScript

Direct style:
```js
element.style.backgroundColor = "lightblue";
element.style.fontSize = "20px";
```

Class-based style:
```js
element.classList.add("active");
element.classList.remove("hidden");
element.classList.toggle("highlight");
```

CSS:
```css
.highlight {
  background-color: #fff3cd;
  font-weight: bold;
}
```

Use camelCase in JavaScript style properties (`backgroundColor`, not `background-color`). In a real project, class-based styling is usually easier to maintain.

## 10. Timers and stopwatch logic

```js
let seconds = 0;
let timerId = null;

function renderTime() {
  const minutes = Math.floor(seconds / 60);
  const remainingSeconds = seconds % 60;
  document.getElementById("display").textContent =
    `${String(minutes).padStart(2, "0")}:${String(remainingSeconds).padStart(2, "0")}`;
}

function start() {
  if (timerId !== null) return; // avoid multiple intervals
  timerId = setInterval(() => {
    seconds += 1;
    renderTime();
  }, 1000);
}

function stop() {
  clearInterval(timerId);
  timerId = null;
}

function reset() {
  stop();
  seconds = 0;
  renderTime();
}
```

The key is storing the interval ID so you can stop it and prevent multiple intervals. For a stopwatch with laps, save a snapshot of the displayed time when the lap button is clicked.

## 11. Dates and currency formatting

```js
const amount = 1234.5;
const formatted = new Intl.NumberFormat("en-GB", {
  style: "currency",
  currency: "GBP"
}).format(amount);
```

`toFixed(2)` returns a string with two decimal places. Use `Intl.NumberFormat` when locale-aware currency formatting is required.

## 12. How to connect separate files

```html
<script src="script.js" defer></script>
```

A useful structure:
```text
project/
├── index.html
├── styles.css
└── script.js
```

Keep HTML IDs, CSS classes, and JavaScript selectors consistent. If an element is `id="output"` in HTML, select `getElementById("output")`, not a different name.

## 13. Worked question: price with discount

**Question pattern:** Read a price and a discount percentage, validate them, and display the final price.

```js
function discountedPrice(price, discountPercent) {
  if (!Number.isFinite(price) || price < 0) {
    throw new Error("Price must be a non-negative number.");
  }
  if (!Number.isFinite(discountPercent) ||
      discountPercent < 0 || discountPercent > 100) {
    throw new Error("Discount must be between 0 and 100.");
  }
  return price * (1 - discountPercent / 100);
}

const finalPrice = discountedPrice(80, 15);
console.log(finalPrice.toFixed(2)); // "68.00"
```

To adapt it to a webpage, read the two input values in a click/submit handler and write the result into an output element.

## 14. Debugging checklist

- Does the selector return the expected element?
- Is the script running after the DOM is available?
- Is the event type correct (`click`, `input`, `change`, `submit`)?
- Are input values converted to numbers where needed?
- Is the selected radio found with `:checked`?
- Are empty/invalid inputs handled?
- Are comparisons using the intended operators?
- Are interval IDs cleared?
- Are CSS property names camelCase in JavaScript?
- Is the console reporting an error before the line you are testing?

## 15. Practice variations

1. Read a score and display a grade.
2. Read two numbers and show their sum.
3. Validate a registration form.
4. Use radio buttons to select a price plan.
5. Filter a list of products by name.
6. Toggle a CSS class when a button is clicked.
7. Build start/stop/reset stopwatch controls and lap snapshots.
8. Calculate a discount and display formatted currency.

**Exam strategy:** write the data flow in plain language first: “When the user does X, read Y, check Z, calculate A, and display B.” Then implement those steps in that order.
