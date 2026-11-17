# Bootstrap

Bootstrap is a popular open-source CSS framework used to build responsive, mobile-first websites. It provides ready-made CSS classes, components, layouts, and JavaScript plugins.

## 1. Installation

### Using npm

```bash
npm install bootstrap
```

### Using CDN

Add Bootstrap CSS inside the HTML `<head>`:

```html
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
  rel="stylesheet"
/>
```

Add Bootstrap JavaScript before the closing `</body>` tag:

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
```

The bundle includes Popper, which is required by components such as dropdowns and tooltips.

## 2. Import Bootstrap in React

Import Bootstrap CSS and JavaScript in your main entry file.

```javascript
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.bundle.min.js";
```

## 3. Container

Bootstrap containers control the width and alignment of page content.

```html
<div class="container">
  <h1>Fixed Width Container</h1>
</div>

<div class="container-fluid">
  <h1>Full Width Container</h1>
</div>
```

Common container classes:

| Class | Purpose |
|---|---|
| `container` | Responsive fixed-width container |
| `container-fluid` | Full-width container |
| `container-sm` | Full width until the small breakpoint |
| `container-md` | Full width until the medium breakpoint |
| `container-lg` | Full width until the large breakpoint |
| `container-xl` | Full width until the extra-large breakpoint |
| `container-xxl` | Full width until the extra-extra-large breakpoint |

## 4. Grid System

Bootstrap uses a 12-column responsive grid system.

```html
<div class="container">
  <div class="row">
    <div class="col-6">Column 1</div>
    <div class="col-6">Column 2</div>
  </div>
</div>
```

### Responsive Grid Classes

| Class | Breakpoint |
|---|---|
| `col-` | All screen sizes |
| `col-sm-` | Small devices |
| `col-md-` | Medium devices |
| `col-lg-` | Large devices |
| `col-xl-` | Extra-large devices |
| `col-xxl-` | Extra-extra-large devices |

Example:

```html
<div class="row">
  <div class="col-12 col-md-6 col-lg-4">
    Column 1
  </div>

  <div class="col-12 col-md-6 col-lg-4">
    Column 2
  </div>

  <div class="col-12 col-md-12 col-lg-4">
    Column 3
  </div>
</div>
```

## 5. Typography

Bootstrap provides predefined typography classes.

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>

<p class="lead">Highlighted paragraph text.</p>

<p class="text-muted">Muted text</p>

<p class="fw-bold">Bold text</p>

<p class="fst-italic">Italic text</p>

<p class="text-uppercase">uppercase text</p>

<p class="text-lowercase">LOWERCASE TEXT</p>

<p class="text-capitalize">capitalize text</p>
```

## 6. Colors

Bootstrap includes predefined text and background color classes.

### Text Colors

```html
<p class="text-primary">Primary</p>
<p class="text-secondary">Secondary</p>
<p class="text-success">Success</p>
<p class="text-danger">Danger</p>
<p class="text-warning">Warning</p>
<p class="text-info">Info</p>
<p class="text-light bg-dark">Light</p>
<p class="text-dark">Dark</p>
<p class="text-white bg-dark">White</p>
```

### Background Colors

```html
<div class="bg-primary text-white">Primary Background</div>
<div class="bg-success text-white">Success Background</div>
<div class="bg-danger text-white">Danger Background</div>
<div class="bg-warning">Warning Background</div>
<div class="bg-info">Info Background</div>
```

## 7. Buttons

Bootstrap provides different button styles.

```html
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-success">Success</button>
<button class="btn btn-danger">Danger</button>
<button class="btn btn-warning">Warning</button>
<button class="btn btn-info">Info</button>
<button class="btn btn-dark">Dark</button>
<button class="btn btn-light">Light</button>
```

### Button Sizes

```html
<button class="btn btn-primary btn-lg">Large Button</button>

<button class="btn btn-primary">Normal Button</button>

<button class="btn btn-primary btn-sm">Small Button</button>
```

### Outline Buttons

```html
<button class="btn btn-outline-primary">Primary</button>
<button class="btn btn-outline-success">Success</button>
<button class="btn btn-outline-danger">Danger</button>
```

## 8. Cards

Cards display content inside a bordered container.

```html
<div class="card" style="width: 18rem;">
  <img src="image.jpg" class="card-img-top" alt="Example">

  <div class="card-body">
    <h5 class="card-title">Card Title</h5>
    <p class="card-text">Some example card content.</p>
    <a href="#" class="btn btn-primary">Read More</a>
  </div>
</div>
```

## 9. Navbar

Create responsive navigation bars.

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container">
    <a class="navbar-brand" href="#">My Website</a>

    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarMenu"
      aria-controls="navbarMenu"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarMenu">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home</a>
        </li>

        <li class="nav-item">
          <a class="nav-link" href="#">About</a>
        </li>

        <li class="nav-item">
          <a class="nav-link" href="#">Contact</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

## 10. Forms

Bootstrap provides styling for input fields, labels, checkboxes, and other form controls.

```html
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input
      type="email"
      class="form-control"
      id="email"
      placeholder="Enter email"
    >
  </div>

  <div class="mb-3">
    <label for="password" class="form-label">Password</label>
    <input
      type="password"
      class="form-control"
      id="password"
    >
  </div>

  <button type="submit" class="btn btn-primary">
    Submit
  </button>
</form>
```

### Common Form Classes

| Class | Purpose |
|---|---|
| `form-control` | Style input fields |
| `form-label` | Style labels |
| `form-select` | Style select dropdowns |
| `form-check` | Style checkbox and radio groups |
| `form-check-input` | Style checkbox or radio input |
| `form-check-label` | Style checkbox or radio label |
| `form-text` | Display help text |
| `input-group` | Combine inputs with buttons or text |

## 11. Tables

Bootstrap provides responsive and styled tables.

```html
<table class="table">
  <thead>
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Email</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>1</td>
      <td>John</td>
      <td>john@example.com</td>
    </tr>
  </tbody>
</table>
```

### Table Classes

```html
<table class="table table-striped">
<table class="table table-bordered">
<table class="table table-hover">
<table class="table table-dark">
<table class="table table-sm">
```

For responsive tables:

```html
<div class="table-responsive">
  <table class="table">
    <!-- Table content -->
  </table>
</div>
```

## 12. Alerts

Display feedback messages to users.

```html
<div class="alert alert-primary">Primary Alert</div>
<div class="alert alert-success">Success Alert</div>
<div class="alert alert-danger">Danger Alert</div>
<div class="alert alert-warning">Warning Alert</div>
<div class="alert alert-info">Info Alert</div>
```

Dismissible alert:

```html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  Warning! Something needs your attention.

  <button
    type="button"
    class="btn-close"
    data-bs-dismiss="alert"
    aria-label="Close"
  ></button>
</div>
```

## 13. Modal

A modal displays content in a popup window.

```html
<button
  class="btn btn-primary"
  data-bs-toggle="modal"
  data-bs-target="#exampleModal"
>
  Open Modal
</button>

<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="modalTitle" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">

      <div class="modal-header">
        <h5 class="modal-title" id="modalTitle">Modal Title</h5>

        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="modal"
          aria-label="Close"
        ></button>
      </div>

      <div class="modal-body">
        This is modal content.
      </div>

      <div class="modal-footer">
        <button class="btn btn-secondary" data-bs-dismiss="modal">
          Close
        </button>

        <button class="btn btn-primary">Save</button>
      </div>

    </div>
  </div>
</div>
```

## 14. Dropdown

```html
<div class="dropdown">
  <button
    class="btn btn-primary dropdown-toggle"
    data-bs-toggle="dropdown"
  >
    Select Option
  </button>

  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Option 1</a></li>
    <li><a class="dropdown-item" href="#">Option 2</a></li>
    <li><a class="dropdown-item" href="#">Option 3</a></li>
  </ul>
</div>
```

## 15. Spacing Utilities

Bootstrap provides margin and padding utility classes.

### Margin

```html
<div class="m-3">All-side margin</div>
<div class="mt-3">Top margin</div>
<div class="mb-3">Bottom margin</div>
<div class="ms-3">Start margin</div>
<div class="me-3">End margin</div>
<div class="mx-3">Horizontal margin</div>
<div class="my-3">Vertical margin</div>
```

### Padding

```html
<div class="p-3">All-side padding</div>
<div class="pt-3">Top padding</div>
<div class="pb-3">Bottom padding</div>
<div class="ps-3">Start padding</div>
<div class="pe-3">End padding</div>
<div class="px-3">Horizontal padding</div>
<div class="py-3">Vertical padding</div>
```

Spacing values generally range from `0` to `5`, with additional options such as `auto` available for applicable margin utilities.

## 16. Display Utilities

Control element display properties.

```html
<div class="d-none">Hidden Element</div>
<div class="d-block">Block Element</div>
<div class="d-inline">Inline Element</div>
<div class="d-flex">Flex Element</div>
<div class="d-grid">Grid Element</div>
```

Responsive display:

```html
<div class="d-none d-md-block">
  Visible on medium screens and larger
</div>

<div class="d-block d-lg-none">
  Visible below large screens
</div>
```

## 17. Flexbox Utilities

```html
<div class="d-flex justify-content-center align-items-center">
  Centered Content
</div>
```

Common classes:

| Class | Purpose |
|---|---|
| `d-flex` | Enable flexbox |
| `flex-row` | Horizontal direction |
| `flex-column` | Vertical direction |
| `justify-content-start` | Align items at the start |
| `justify-content-center` | Center items horizontally |
| `justify-content-end` | Align items at the end |
| `justify-content-between` | Space items between |
| `align-items-center` | Center items vertically |
| `flex-wrap` | Allow items to wrap |
| `gap-3` | Add spacing between items |

## 18. Position Utilities

```html
<div class="position-relative">
  Relative Element
</div>

<div class="position-absolute top-0 end-0">
  Absolute Element
</div>

<div class="position-fixed bottom-0 end-0">
  Fixed Element
</div>

<div class="position-sticky top-0">
  Sticky Element
</div>
```

## 19. Bootstrap Icons

Bootstrap Icons is a separate icon library.

### Installation

```bash
npm install bootstrap-icons
```

### Import CSS

```javascript
import "bootstrap-icons/font/bootstrap-icons.css";
```

### Example

```html
<i class="bi bi-house"></i>
<i class="bi bi-person"></i>
<i class="bi bi-search"></i>
<i class="bi bi-trash"></i>
<i class="bi bi-heart"></i>
```

## 20. Bootstrap with React

Bootstrap CSS classes can be used directly inside React components.

```jsx
function App() {
  return (
    <div className="container mt-5">
      <h1 className="text-primary">Welcome to React</h1>

      <button className="btn btn-success">
        Click Me
      </button>
    </div>
  );
}

export default App;
```

**Note:** In React JSX, use `className` instead of `class`.

## 21. React-Bootstrap

React-Bootstrap provides Bootstrap components implemented as React components.

### Installation

```bash
npm install react-bootstrap bootstrap
```

### Import CSS

```javascript
import "bootstrap/dist/css/bootstrap.min.css";
```

### Example

```jsx
import Button from "react-bootstrap/Button";
import Card from "react-bootstrap/Card";

function App() {
  return (
    <Card style={{ width: "18rem" }}>
      <Card.Body>
        <Card.Title>React Bootstrap</Card.Title>

        <Card.Text>
          Build responsive React applications.
        </Card.Text>

        <Button variant="primary">
          Learn More
        </Button>
      </Card.Body>
    </Card>
  );
}

export default App;
```

## 22. Common Bootstrap Components

| Component | Purpose |
|---|---|
| Navbar | Website navigation |
| Card | Display grouped content |
| Button | Interactive buttons |
| Modal | Popup windows |
| Dropdown | Dropdown menus |
| Alert | Feedback messages |
| Carousel | Image and content slider |
| Accordion | Expandable content |
| Tooltip | Contextual information |
| Popover | Small content popup |
| Offcanvas | Sliding sidebar |
| Pagination | Navigate between pages |
| Breadcrumb | Display navigation hierarchy |
| Badge | Display labels and counts |
| Progress | Show progress status |
| Spinner | Loading indicator |

## 23. Important Notes

- Bootstrap is mobile-first and responsive.
- The grid system uses 12 columns.
- Use containers and rows to organize layouts.
- Use utility classes to reduce custom CSS.
- Bootstrap JavaScript components require the Bootstrap JavaScript bundle.
- React applications can use Bootstrap CSS directly or use React-Bootstrap components.
- Bootstrap CSS classes use `class` in HTML and `className` in React JSX.

## Official Documentation

- Bootstrap: https://getbootstrap.com/
- Bootstrap Components: https://getbootstrap.com/docs/5.3/components/
- Bootstrap Utilities: https://getbootstrap.com/docs/5.3/utilities/
- Bootstrap Icons: https://icons.getbootstrap.com/
- React-Bootstrap: https://react-bootstrap.github.io/