# Bootstrap Functional Guide

This guide provides comprehensive documentation of Bootstrap's features, configuration options, and functional specifications.

## Feature Documentation and Use Cases

### 1. Grid System

#### Overview
Bootstrap's grid system uses a series of containers, rows, and columns to layout and align content. It's built with flexbox and is fully responsive.

#### Configuration Options

**Container Types:**
- `.container`: Fixed-width responsive container
- `.container-fluid`: Full-width container
- `.container-{breakpoint}`: 100% wide until specified breakpoint

**Grid Breakpoints:**
```scss
$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
  xxl: 1400px
);
```

**Column Classes:**
- `.col`: Equal-width columns
- `.col-{breakpoint}`: Responsive column at breakpoint
- `.col-{breakpoint}-{number}`: Specific width (1-12)
- `.col-auto`: Column sized by content

#### Use Case: Responsive Three-Column Layout

```html
<div class="container">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Full width on mobile, half on tablet, third on desktop -->
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Content -->
    </div>
    <div class="col-12 col-md-12 col-lg-4">
      <!-- Content -->
    </div>
  </div>
</div>
```

**Customization:**
```scss
// Override grid variables
$grid-columns: 12;
$grid-gutter-width: 1.5rem;
$grid-row-columns: 6;
```

#### Input/Output Specifications

**Input:** HTML structure with grid classes  
**Output:** Responsive layout that adapts to viewport width  
**Validation:** Columns must sum to 12 or use `col-auto`

---

### 2. Component: Buttons

#### Overview
Bootstrap provides extensive button styles, sizes, and states for various use cases.

#### Configuration Options

**Button Variants:**
- `btn-primary`: Primary action button
- `btn-secondary`: Secondary action
- `btn-success`: Success state
- `btn-danger`: Danger/delete action
- `btn-warning`: Warning action
- `btn-info`: Informational
- `btn-light`: Light background
- `btn-dark`: Dark background
- `btn-link`: Link-styled button

**Button Sizes:**
- `btn-lg`: Large button
- Default: Regular size
- `btn-sm`: Small button

**Button States:**
- `active`: Active state
- `disabled`: Disabled state (via attribute or class)

#### Use Cases

**Single Action Button:**
```html
<button type="button" class="btn btn-primary">Save Changes</button>
```

**Button Group:**
```html
<div class="btn-group" role="group">
  <button type="button" class="btn btn-primary">Left</button>
  <button type="button" class="btn btn-primary">Middle</button>
  <button type="button" class="btn btn-primary">Right</button>
</div>
```

**Loading State:**
```html
<button class="btn btn-primary" type="button" disabled>
  <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
  Loading...
</button>
```

#### Customization

```scss
// Button variables
$btn-padding-y: 0.375rem;
$btn-padding-x: 0.75rem;
$btn-border-radius: 0.25rem;
$btn-font-size: 1rem;
```

**JavaScript API:**
```javascript
// Toggle button state
const button = document.getElementById('myButton');
button.addEventListener('click', function () {
  this.classList.toggle('active');
});
```

---

### 3. Component: Modal

#### Overview
Modals are dialog boxes/popups that display content over the current page.

#### Configuration Options

**JavaScript Options:**
```javascript
const modal = new bootstrap.Modal(element, {
  backdrop: true,      // true | false | 'static'
  keyboard: true,      // Close on ESC key
  focus: true,         // Focus modal on init
  show: false          // Show modal on init
});
```

**Sizes:**
- `modal-sm`: Small modal (300px)
- Default: Regular modal (500px)
- `modal-lg`: Large modal (800px)
- `modal-xl`: Extra large (1140px)
- `modal-fullscreen`: Full screen modal

**Variations:**
- Centered: `modal-dialog-centered`
- Scrollable: `modal-dialog-scrollable`
- Static backdrop: `data-bs-backdrop="static"`

#### Use Case: Confirmation Dialog

```html
<!-- Button trigger -->
<button type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#deleteModal">
  Delete Item
</button>

<!-- Modal -->
<div class="modal fade" id="deleteModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Confirm Deletion</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        Are you sure you want to delete this item?
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        <button type="button" class="btn btn-danger">Delete</button>
      </div>
    </div>
  </div>
</div>
```

#### JavaScript API

```javascript
// Programmatic control
const myModal = new bootstrap.Modal('#myModal');

// Methods
myModal.show();      // Show modal
myModal.hide();      // Hide modal
myModal.toggle();    // Toggle modal
myModal.dispose();   // Destroy modal instance

// Events
element.addEventListener('show.bs.modal', function (event) {
  console.log('Modal is about to be shown');
});

element.addEventListener('hidden.bs.modal', function (event) {
  console.log('Modal is now hidden');
});
```

**Events:**
- `show.bs.modal`: Fired when show method is called
- `shown.bs.modal`: Fired when modal is fully visible
- `hide.bs.modal`: Fired when hide method is called
- `hidden.bs.modal`: Fired when modal is fully hidden

---

### 4. Component: Forms

#### Overview
Bootstrap provides comprehensive form styling and validation capabilities.

#### Form Controls

**Input Types:**
```html
<input type="text" class="form-control" placeholder="Text input">
<input type="email" class="form-control" placeholder="Email">
<input type="password" class="form-control" placeholder="Password">
<textarea class="form-control" rows="3"></textarea>
<select class="form-select">
  <option>Choose...</option>
  <option>Option 1</option>
</select>
```

**Sizes:**
- `form-control-lg`: Large input
- `form-control`: Default size
- `form-control-sm`: Small input

#### Validation

**HTML5 Validation:**
```html
<form class="needs-validation" novalidate>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input type="email" class="form-control" id="email" required>
    <div class="invalid-feedback">
      Please provide a valid email.
    </div>
  </div>
  <button class="btn btn-primary" type="submit">Submit</button>
</form>

<script>
// Enable validation
(function () {
  'use strict'
  const forms = document.querySelectorAll('.needs-validation')
  Array.from(forms).forEach(form => {
    form.addEventListener('submit', event => {
      if (!form.checkValidity()) {
        event.preventDefault()
        event.stopPropagation()
      }
      form.classList.add('was-validated')
    }, false)
  })
})()
</script>
```

**Server-side Validation:**
```html
<input type="text" class="form-control is-invalid" value="incorrect-value">
<div class="invalid-feedback">
  This field is required.
</div>

<input type="text" class="form-control is-valid" value="correct-value">
<div class="valid-feedback">
  Looks good!
</div>
```

#### Input Groups

```html
<div class="input-group">
  <span class="input-group-text">@</span>
  <input type="text" class="form-control" placeholder="Username">
</div>

<div class="input-group">
  <input type="text" class="form-control" placeholder="Amount">
  <span class="input-group-text">.00</span>
</div>

<div class="input-group">
  <button class="btn btn-outline-secondary" type="button">Button</button>
  <input type="text" class="form-control">
</div>
```

#### Floating Labels

```html
<div class="form-floating mb-3">
  <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
  <label for="floatingInput">Email address</label>
</div>
```

---

### 5. Component: Dropdown

#### Overview
Toggleable contextual overlay for displaying lists of links.

#### Configuration Options

**JavaScript Options:**
```javascript
const dropdown = new bootstrap.Dropdown(element, {
  offset: [0, 2],           // Offset from reference element
  boundary: 'clippingParents', // Overflow boundary
  reference: 'toggle',      // Reference element
  display: 'dynamic',       // Dynamic positioning
  popperConfig: null,       // Custom Popper config
  autoClose: true           // true | false | 'inside' | 'outside'
});
```

#### Use Cases

**Basic Dropdown:**
```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" 
          data-bs-toggle="dropdown" aria-expanded="false">
    Dropdown button
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
    <li><hr class="dropdown-divider"></li>
    <li><a class="dropdown-item" href="#">Separated link</a></li>
  </ul>
</div>
```

**Dropdown Directions:**
```html
<!-- Dropup -->
<div class="dropup">
  <button class="btn btn-secondary dropdown-toggle" data-bs-toggle="dropdown">
    Dropup
  </button>
  <ul class="dropdown-menu">...</ul>
</div>

<!-- Dropend -->
<div class="dropend">
  <button class="btn btn-secondary dropdown-toggle" data-bs-toggle="dropdown">
    Dropend
  </button>
  <ul class="dropdown-menu">...</ul>
</div>

<!-- Dropstart -->
<div class="dropstart">
  <button class="btn btn-secondary dropdown-toggle" data-bs-toggle="dropdown">
    Dropstart
  </button>
  <ul class="dropdown-menu">...</ul>
</div>
```

---

### 6. Component: Carousel

#### Overview
Cycling through elements (images or slides of text) like a carousel.

#### Configuration Options

**JavaScript Options:**
```javascript
const carousel = new bootstrap.Carousel(element, {
  interval: 5000,        // Time between slides (ms), false to disable
  keyboard: true,        // Respond to keyboard events
  pause: 'hover',        // 'hover' | false - pause on hover
  ride: false,           // 'carousel' to autoplay on load
  wrap: true,            // Cycle continuously
  touch: true            // Enable touch swipe gestures
});
```

#### Use Case: Image Slider

```html
<div id="carouselExample" class="carousel slide" data-bs-ride="carousel">
  <!-- Indicators -->
  <div class="carousel-indicators">
    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="0" class="active"></button>
    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="1"></button>
    <button type="button" data-bs-target="#carouselExample" data-bs-slide-to="2"></button>
  </div>
  
  <!-- Slides -->
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="slide1.jpg" class="d-block w-100" alt="Slide 1">
      <div class="carousel-caption">
        <h5>First slide label</h5>
        <p>Some description</p>
      </div>
    </div>
    <div class="carousel-item">
      <img src="slide2.jpg" class="d-block w-100" alt="Slide 2">
    </div>
    <div class="carousel-item">
      <img src="slide3.jpg" class="d-block w-100" alt="Slide 3">
    </div>
  </div>
  
  <!-- Controls -->
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#carouselExample" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>
```

**JavaScript API:**
```javascript
const myCarousel = new bootstrap.Carousel('#myCarousel');

// Methods
myCarousel.cycle();              // Cycle through items
myCarousel.pause();              // Stop cycling
myCarousel.prev();               // Go to previous
myCarousel.next();               // Go to next
myCarousel.nextWhenVisible();    // Next when visible
myCarousel.to(2);                // Go to specific slide (0-indexed)
```

---

### 7. Component: Toast

#### Overview
Lightweight notifications designed to mimic push notifications.

#### Configuration Options

```javascript
const toast = new bootstrap.Toast(element, {
  animation: true,    // Apply CSS fade transition
  autohide: true,     // Auto hide toast
  delay: 5000         // Delay before hiding (ms)
});
```

#### Use Case: Notification System

```html
<!-- Toast container -->
<div class="toast-container position-fixed top-0 end-0 p-3">
  <div id="liveToast" class="toast" role="alert">
    <div class="toast-header">
      <strong class="me-auto">Bootstrap</strong>
      <small>11 mins ago</small>
      <button type="button" class="btn-close" data-bs-dismiss="toast"></button>
    </div>
    <div class="toast-body">
      Hello, world! This is a toast message.
    </div>
  </div>
</div>

<script>
// Show toast
const toastElement = document.getElementById('liveToast');
const toast = new bootstrap.Toast(toastElement);
toast.show();

// Or trigger via button
document.getElementById('showToastBtn').addEventListener('click', function() {
  toast.show();
});
</script>
```

**Color Schemes:**
```html
<div class="toast align-items-center text-bg-primary">
  <div class="d-flex">
    <div class="toast-body">Primary toast</div>
    <button type="button" class="btn-close btn-close-white me-2 m-auto"></button>
  </div>
</div>
```

---

### 8. Utilities: Spacing

#### Overview
Responsive spacing utilities for margins and padding.

#### Syntax

```
{property}{sides}-{size}
{property}{sides}-{breakpoint}-{size}
```

**Property:**
- `m`: margin
- `p`: padding

**Sides:**
- `t`: top
- `b`: bottom
- `s`: start (left in LTR)
- `e`: end (right in LTR)
- `x`: left and right
- `y`: top and bottom
- blank: all sides

**Size:**
- `0`: 0
- `1`: $spacer * 0.25
- `2`: $spacer * 0.5
- `3`: $spacer * 1
- `4`: $spacer * 1.5
- `5`: $spacer * 3
- `auto`: auto

#### Examples

```html
<div class="mt-3">Margin top 1rem</div>
<div class="px-4">Padding left and right 1.5rem</div>
<div class="mb-5">Margin bottom 3rem</div>
<div class="m-0">No margin</div>
<div class="mx-auto">Centered with auto margin</div>

<!-- Responsive -->
<div class="mt-3 mt-md-5">Margin top 1rem on mobile, 3rem on tablet+</div>
```

---

### 9. Utilities: Display

#### Overview
Responsive display utilities for showing/hiding elements.

#### Display Values

```html
<div class="d-none">Hidden on all</div>
<div class="d-block">Block on all</div>
<div class="d-inline">Inline on all</div>
<div class="d-inline-block">Inline-block on all</div>
<div class="d-flex">Flex container on all</div>
<div class="d-grid">Grid container on all</div>

<!-- Responsive -->
<div class="d-none d-md-block">Hidden on mobile, visible on tablet+</div>
<div class="d-block d-md-none">Visible on mobile, hidden on tablet+</div>
```

---

### 10. Utilities: Flexbox

#### Overview
Quickly manage layout, alignment, and sizing with flex utilities.

#### Direction

```html
<div class="d-flex flex-row">Horizontal (default)</div>
<div class="d-flex flex-row-reverse">Horizontal reversed</div>
<div class="d-flex flex-column">Vertical</div>
<div class="d-flex flex-column-reverse">Vertical reversed</div>
```

#### Justify Content

```html
<div class="d-flex justify-content-start">Start</div>
<div class="d-flex justify-content-end">End</div>
<div class="d-flex justify-content-center">Center</div>
<div class="d-flex justify-content-between">Space between</div>
<div class="d-flex justify-content-around">Space around</div>
<div class="d-flex justify-content-evenly">Space evenly</div>
```

#### Align Items

```html
<div class="d-flex align-items-start">Top</div>
<div class="d-flex align-items-end">Bottom</div>
<div class="d-flex align-items-center">Center</div>
<div class="d-flex align-items-baseline">Baseline</div>
<div class="d-flex align-items-stretch">Stretch (default)</div>
```

---

## Validation Rules and Constraints

### Form Validation Constraints

1. **Required Fields**: Must have non-empty value
2. **Email**: Must match email format pattern
3. **URL**: Must be valid URL format
4. **Number**: Must be numeric within min/max range
5. **Pattern**: Must match custom regex pattern
6. **Min Length**: Minimum character count
7. **Max Length**: Maximum character count

### Component Constraints

1. **Modal**: Only one modal can be open at a time
2. **Dropdown**: Must have toggle element
3. **Carousel**: Minimum 1 slide required
4. **Grid**: Columns should sum to 12
5. **Toast**: Maximum recommended: 5 concurrent toasts

## Feature Dependencies

### CSS-Only Components (No JavaScript)
- Alerts (static)
- Badges
- Breadcrumbs
- Buttons (static)
- Cards
- List groups
- Progress bars
- Spinners (static)

### JavaScript-Required Components
- Carousel
- Collapse
- Dropdowns
- Modals
- Offcanvas
- Popovers
- Scrollspy
- Tabs
- Toasts
- Tooltips

### Popper.js-Dependent Components
- Dropdowns
- Popovers
- Tooltips

## Customization Guide

### Sass Variables

```scss
// Override before importing Bootstrap
$primary: #0074d9;
$secondary: #6c757d;
$success: #28a745;

// Spacing
$spacer: 1rem;

// Typography
$font-family-base: 'Helvetica Neue', Arial, sans-serif;
$font-size-base: 1rem;
$line-height-base: 1.5;

// Border radius
$border-radius: 0.25rem;
$border-radius-lg: 0.5rem;
$border-radius-sm: 0.125rem;

// Import Bootstrap
@import "bootstrap/scss/bootstrap";
```

### Component-Specific Variables

```scss
// Buttons
$btn-padding-y: 0.375rem;
$btn-padding-x: 0.75rem;
$btn-font-size: 1rem;
$btn-border-radius: 0.25rem;

// Modals
$modal-inner-padding: 1rem;
$modal-dialog-margin: 0.5rem;
$modal-content-border-radius: 0.3rem;

// Forms
$input-padding-y: 0.375rem;
$input-padding-x: 0.75rem;
$input-border-radius: 0.25rem;
$input-focus-border-color: tint-color($primary, 50%);
```

---

*This functional guide provides comprehensive documentation of Bootstrap's features and configuration options. For additional details, refer to the official Bootstrap documentation.*
