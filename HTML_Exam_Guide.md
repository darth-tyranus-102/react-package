# HTML Exam-Solving Guide
**Web Programming | Weeks 5–8 foundations, connected to the later React exercises**

> Use this guide to build pages from a question, not just remember tags. The weekly materials include profile pages, event pages, footers, forms, lists, tables, links, and HTML that connects to CSS and JavaScript.

## 1. Turn the question into a page plan

Before writing code, underline the required content and map each item to an HTML element.

| Requirement in a question | Likely element/pattern |
|---|---|
| Main page heading | `<h1>` |
| Section heading | `<h2>` or `<h3>` |
| Paragraph or description | `<p>` |
| A sequence of items | `<ul><li>` or `<ol><li>` |
| Navigation or external destination | `<a href="...">` |
| Image | `<img src="..." alt="...">` |
| Header, main content, footer | `<header>`, `<main>`, `<footer>` |
| Independent article or profile | `<article>` |
| Group of related content | `<section>` |
| Collect user input | `<form>` with labels and controls |
| Data arranged in rows/columns | `<table>` |
| Connect CSS | `<link rel="stylesheet" href="styles.css">` |
| Load JavaScript | `<script src="script.js" defer></script>` |

Semantic elements explain the role of the content. Use them where appropriate rather than placing every part inside a generic `<div>`.

## 2. Reliable HTML document skeleton

Start with this, then add the content the question requests.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link rel="stylesheet" href="styles.css">
  <script src="script.js" defer></script>
</head>
<body>
  <header>
    <h1>Page Heading</h1>
  </header>

  <main>
    <section>
      <h2>Section Heading</h2>
      <p>Section content.</p>
    </section>
  </main>

  <footer>
    <p>&copy; 2026 Example Site</p>
  </footer>
</body>
</html>
```

If the question asks for HTML only, omit the CSS/JS links if they are not needed. If it asks for separate files, do not put all code into one file.

## 3. Lists, links, images, and page sections

```html
<section id="speakers">
  <h2>Speakers</h2>
  <ul id="speakerList">
    <li>
      <img src="speaker.jpg" alt="Portrait of the speaker">
      <a href="speaker-profile.html">View speaker profile</a>
    </li>
    <li>Second speaker</li>
  </ul>
</section>
```

- `id` identifies one unique element; CSS/JS can target it with `#speakers`.
- `class` is reusable; CSS can target it with `.card`.
- `href` is the destination of a link; `src` is the path to a resource.
- `alt` describes an image for accessibility and when the image cannot load.
- Use relative paths such as `images/logo.png` only when the folder structure matches the path.

## 4. Forms: a reusable pattern

```html
<form id="registrationForm">
  <div>
    <label for="fullName">Full name</label>
    <input id="fullName" name="fullName" type="text" required>
  </div>

  <div>
    <label for="email">Email</label>
    <input id="email" name="email" type="email" required>
  </div>

  <fieldset>
    <legend>Attendance type</legend>
    <label>
      <input type="radio" name="attendance" value="online" required>
      Online
    </label>
    <label>
      <input type="radio" name="attendance" value="in-person">
      In person
    </label>
  </fieldset>

  <label>
    <input type="checkbox" name="updates">
    Send me updates
  </label>

  <button type="submit">Register</button>
</form>
```

Important distinctions:
- Radio buttons that belong to one choice group must share the same `name`.
- Checkboxes are appropriate when zero, one, or multiple independent options may be selected.
- `required`, `type="email"`, `min`, `max`, and `minlength` provide browser-level validation.
- A `<label for="...">` must match the input's `id`.
- A form button defaults to submit in many contexts; explicitly use `type="button"` for a button that should not submit the form.

## 5. Tables

Use a table for genuinely tabular data, not general page layout.

```html
<table>
  <thead>
    <tr>
      <th scope="col">Product</th>
      <th scope="col">Price</th>
      <th scope="col">Stock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Notebook</td>
      <td>£3.50</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
```

Remember the hierarchy: `table` → `thead`/`tbody` → `tr` → `th`/`td`.

## 6. Common exam task: profile/event page

**Question pattern:** Create a page with a heading, an about section, a list of items, and a footer.

```html
<header class="site-header">
  <h1>Tech Innovators Summit</h1>
</header>

<main>
  <section id="about">
    <h2>About the Event</h2>
    <p>Meet developers and explore new technologies.</p>
  </section>

  <section id="agenda">
    <h2>Agenda</h2>
    <ol>
      <li>Registration</li>
      <li>Opening talk</li>
      <li>Panel discussion</li>
    </ol>
  </section>
</main>

<footer>
  <p>Contact: events@example.com</p>
</footer>
```

**How to adapt it:** Replace the text, change the list type, add a speaker section, or add links/images. Keep the structure and change only what the question requires.

## 7. How HTML fits into a wider project

A simple project can be arranged as:

```text
project/
├── index.html
├── styles.css
├── script.js
└── images/
    └── logo.png
```

HTML provides structure; CSS provides presentation; JavaScript adds behaviour. Connect them with exact file paths:

```html
<link rel="stylesheet" href="styles.css">
<script src="script.js" defer></script>
```

`defer` makes an external script run after HTML parsing, which usually avoids trying to select elements before they exist.

## 8. Debugging checklist

- Is every opening tag closed?
- Are tags nested correctly?
- Is the `id` unique?
- Does each label's `for` match an input `id`?
- Do radio options that belong together share the same `name`?
- Are `href`, `src`, and CSS/JS paths correct?
- Is the content in the correct semantic element?
- Is the page responsive (`meta viewport`)?
- Does the browser console or developer tools show a missing file or malformed markup?

## 9. Practice variations

Try writing the page without looking at the example:
1. A personal profile with hobbies and contact details.
2. An event page with an ordered agenda and speaker list.
3. A product table with name, price, and stock.
4. A registration form with text, email, radio, checkbox, and submit controls.
5. A footer with social links and copyright.

For each, first list the required elements, then write the skeleton, then add IDs/classes only where CSS or JavaScript needs them.

## 10. Last-minute reference

```html
<h1>Main heading</h1>
<section id="about">...</section>
<p>Text</p>
<ul><li>Item</li></ul>
<a href="page.html">Open</a>
<img src="image.png" alt="Description">
<label for="email">Email</label>
<input id="email" type="email" required>
<button type="submit">Submit</button>
```

**Exam strategy:** satisfy every stated requirement first; improve styling and extras only after the required structure is present.
