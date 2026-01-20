# Bootstrap Developer Guide

A comprehensive technical guide for developers working with or contributing to Bootstrap.

## Getting Started

### Prerequisites

- Node.js 18.x or higher
- npm 9.x or higher
- Git 2.x or higher
- Modern code editor (VS Code, WebStorm, etc.)

### Installation

#### Option 1: Using npm (Recommended)

```bash
npm install bootstrap@5.3.8
```

#### Option 2: Using yarn

```bash
yarn add bootstrap@5.3.8
```

#### Option 3: Using CDN

```html
<!-- CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- JavaScript Bundle with Popper -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
```

#### Option 4: Download Source

```bash
git clone https://github.com/twbs/bootstrap.git
cd bootstrap
npm install
npm run dist
```

---

## API Reference

### JavaScript Components API

All Bootstrap JavaScript components follow a consistent API pattern:

#### Component Initialization

**Via Data Attributes (Declarative):**
```html
<button type="button" class="btn btn-primary" 
        data-bs-toggle="modal" 
        data-bs-target="#myModal">
  Launch Modal
</button>
```

**Via JavaScript (Programmatic):**
```javascript
const modal = new bootstrap.Modal('#myModal', {
  keyboard: false,
  backdrop: 'static'
});
```

#### Common Methods

All components support these methods:

```javascript
const instance = bootstrap.ComponentName.getInstance(element);  // Get existing instance
const instance = bootstrap.ComponentName.getOrCreateInstance(element);  // Get or create
instance.dispose();  // Destroy component instance
```

---

### Modal Component

#### Constructor Options

```javascript
const modal = new bootstrap.Modal(element, {
  backdrop: true,    // boolean | 'static' - Include backdrop, 'static' prevents closing on click
  keyboard: true,    // boolean - Close on ESC key press
  focus: true,       // boolean - Put focus on modal when initialized
  show: false        // boolean - Show modal on initialization
});
```

#### Methods

```javascript
modal.show();         // Manually opens modal
modal.hide();         // Manually hides modal
modal.toggle();       // Toggles modal visibility
modal.handleUpdate(); // Readjust modal positioning
modal.dispose();      // Destroys modal instance
```

#### Events

```javascript
const modalElement = document.getElementById('myModal');

modalElement.addEventListener('show.bs.modal', function (event) {
  // Fired immediately when show() is called
  console.log('About to show modal');
  
  // Access related target (button that triggered modal)
  console.log(event.relatedTarget);
  
  // Prevent modal from showing
  // event.preventDefault();
});

modalElement.addEventListener('shown.bs.modal', function (event) {
  // Fired when modal is fully visible (after CSS transitions)
  console.log('Modal is now visible');
});

modalElement.addEventListener('hide.bs.modal', function (event) {
  // Fired immediately when hide() is called
  console.log('About to hide modal');
});

modalElement.addEventListener('hidden.bs.modal', function (event) {
  // Fired when modal is fully hidden (after CSS transitions)
  console.log('Modal is now hidden');
});

modalElement.addEventListener('hidePrevented.bs.modal', function (event) {
  // Fired when modal is shown and backdrop is static
  console.log('Hide prevented by static backdrop');
});
```

#### Code Examples

**Dynamic Modal with Data:**

```javascript
const myModal = document.getElementById('myModal');
const modalTitle = myModal.querySelector('.modal-title');
const modalBody = myModal.querySelector('.modal-body');

myModal.addEventListener('show.bs.modal', function (event) {
  // Button that triggered the modal
  const button = event.relatedTarget;
  
  // Extract info from data-bs-* attributes
  const recipient = button.getAttribute('data-bs-whatever');
  
  // Update modal content
  modalTitle.textContent = `New message to ${recipient}`;
  modalBody.querySelector('input').value = recipient;
});
```

---

### Dropdown Component

#### Constructor Options

```javascript
const dropdown = new bootstrap.Dropdown(element, {
  offset: [0, 2],              // [skidding, distance] from reference element
  boundary: 'clippingParents', // Overflow constraint boundary
  reference: 'toggle',         // Reference element
  display: 'dynamic',          // Enable dynamic positioning
  popperConfig: null,          // Custom Popper configuration
  autoClose: true              // true | false | 'inside' | 'outside'
});
```

#### Methods

```javascript
dropdown.show();      // Show dropdown
dropdown.hide();      // Hide dropdown
dropdown.toggle();    // Toggle dropdown
dropdown.update();    // Update Popper positioning
dropdown.dispose();   // Destroy dropdown instance
```

#### Events

```javascript
element.addEventListener('show.bs.dropdown', function (event) {
  // Cancelable, fires before dropdown is shown
});

element.addEventListener('shown.bs.dropdown', function (event) {
  // Fires after dropdown is shown
});

element.addEventListener('hide.bs.dropdown', function (event) {
  // Cancelable, fires before dropdown is hidden
  // Access the click event that triggered hiding
  console.log(event.clickEvent);
});

element.addEventListener('hidden.bs.dropdown', function (event) {
  // Fires after dropdown is hidden
});
```

#### Code Examples

**Programmatic Control:**

```javascript
// Get dropdown instance
const dropdownElement = document.getElementById('myDropdown');
const dropdown = bootstrap.Dropdown.getInstance(dropdownElement);

// Control via buttons
document.getElementById('showBtn').addEventListener('click', () => {
  dropdown.show();
});

document.getElementById('hideBtn').addEventListener('click', () => {
  dropdown.hide();
});
```

**Custom Popper Configuration:**

```javascript
const dropdown = new bootstrap.Dropdown(element, {
  popperConfig: {
    strategy: 'fixed',
    modifiers: [
      {
        name: 'offset',
        options: {
          offset: [0, 10]
        }
      }
    ]
  }
});
```

---

### Carousel Component

#### Constructor Options

```javascript
const carousel = new bootstrap.Carousel(element, {
  interval: 5000,     // Time between slides (ms), false to disable auto-cycle
  keyboard: true,     // Whether carousel responds to keyboard events
  pause: 'hover',     // 'hover' | false - Pause on mouse enter
  ride: false,        // 'carousel' to autoplay on load
  wrap: true,         // Whether to cycle continuously
  touch: true         // Whether to support touch gestures
});
```

#### Methods

```javascript
carousel.cycle();           // Cycle through items from left to right
carousel.pause();           // Stop cycling through items
carousel.prev();            // Cycle to previous item
carousel.next();            // Cycle to next item
carousel.nextWhenVisible(); // Cycle to next when page is visible
carousel.to(2);             // Cycle to specific slide (0-indexed)
carousel.dispose();         // Destroy carousel instance
```

#### Events

```javascript
element.addEventListener('slide.bs.carousel', function (event) {
  // Fires immediately when slide() is called
  console.log('From:', event.from);      // Index of current slide
  console.log('To:', event.to);          // Index of target slide
  console.log('Direction:', event.direction);  // 'left' or 'right'
});

element.addEventListener('slid.bs.carousel', function (event) {
  // Fires after slide transition completes
});
```

#### Code Examples

**Carousel with Thumbnails:**

```javascript
const carousel = new bootstrap.Carousel('#myCarousel');
const thumbnails = document.querySelectorAll('.thumbnail');

thumbnails.forEach((thumb, index) => {
  thumb.addEventListener('click', () => {
    carousel.to(index);
  });
});

// Update active thumbnail
document.getElementById('myCarousel').addEventListener('slid.bs.carousel', function (event) {
  thumbnails.forEach(t => t.classList.remove('active'));
  thumbnails[event.to].classList.add('active');
});
```

---

### Toast Component

#### Constructor Options

```javascript
const toast = new bootstrap.Toast(element, {
  animation: true,    // Apply CSS fade transition
  autohide: true,     // Auto hide toast
  delay: 5000         // Delay in milliseconds before hiding
});
```

#### Methods

```javascript
toast.show();       // Show toast
toast.hide();       // Hide toast
toast.dispose();    // Destroy toast instance
```

#### Events

```javascript
element.addEventListener('show.bs.toast', function (event) {
  // Fires immediately when show() is called
});

element.addEventListener('shown.bs.toast', function (event) {
  // Fires when toast is fully visible
});

element.addEventListener('hide.bs.toast', function (event) {
  // Fires immediately when hide() is called
});

element.addEventListener('hidden.bs.toast', function (event) {
  // Fires when toast is fully hidden
});
```

#### Code Examples

**Toast Notification System:**

```javascript
class ToastNotification {
  constructor(containerId) {
    this.container = document.getElementById(containerId);
  }
  
  show(message, type = 'info', delay = 5000) {
    const toastId = `toast-${Date.now()}`;
    const toastHTML = `
      <div id="${toastId}" class="toast align-items-center text-bg-${type}" role="alert">
        <div class="d-flex">
          <div class="toast-body">${message}</div>
          <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
        </div>
      </div>
    `;
    
    this.container.insertAdjacentHTML('beforeend', toastHTML);
    
    const toastElement = document.getElementById(toastId);
    const toast = new bootstrap.Toast(toastElement, { delay });
    toast.show();
    
    // Remove from DOM after hidden
    toastElement.addEventListener('hidden.bs.toast', () => {
      toastElement.remove();
    });
  }
}

// Usage
const notifier = new ToastNotification('toast-container');
notifier.show('Profile updated successfully!', 'success');
notifier.show('An error occurred', 'danger');
```

---

### Tooltip Component

#### Constructor Options

```javascript
const tooltip = new bootstrap.Tooltip(element, {
  animation: true,        // Apply CSS fade transition
  container: false,       // Append tooltip to specific element
  delay: 0,              // Delay in ms (can be object: { show: 500, hide: 100 })
  html: false,           // Allow HTML in tooltip
  placement: 'top',      // 'auto' | 'top' | 'bottom' | 'left' | 'right'
  selector: false,       // Delegation selector
  template: '<div class="tooltip" role="tooltip">...</div>',
  title: '',             // Default title
  trigger: 'hover focus', // How tooltip is triggered
  fallbackPlacements: ['top', 'right', 'bottom', 'left'],
  boundary: 'clippingParents',
  customClass: '',       // Add custom classes
  sanitize: true,        // Enable/disable sanitization
  sanitizeFn: null,      // Custom sanitization function
  popperConfig: null     // Custom Popper config
});
```

#### Methods

```javascript
tooltip.show();          // Show tooltip
tooltip.hide();          // Hide tooltip
tooltip.toggle();        // Toggle tooltip
tooltip.enable();        // Enable tooltip
tooltip.disable();       // Disable tooltip
tooltip.toggleEnabled(); // Toggle enabled state
tooltip.update();        // Update Popper position
tooltip.dispose();       // Destroy tooltip
```

#### Events

```javascript
element.addEventListener('show.bs.tooltip', function (event) {
  // Fires immediately when show() is called
});

element.addEventListener('shown.bs.tooltip', function (event) {
  // Fires when tooltip is fully visible
});

element.addEventListener('hide.bs.tooltip', function (event) {
  // Fires immediately when hide() is called
});

element.addEventListener('hidden.bs.tooltip', function (event) {
  // Fires when tooltip is fully hidden
});

element.addEventListener('inserted.bs.tooltip', function (event) {
  // Fires after template is inserted into DOM
});
```

#### Code Examples

**Initialize All Tooltips:**

```javascript
// Enable all tooltips on page
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
const tooltipList = [...tooltipTriggerList].map(tooltipTriggerEl => 
  new bootstrap.Tooltip(tooltipTriggerEl)
);
```

**Dynamic Tooltip Content:**

```javascript
const tooltip = new bootstrap.Tooltip(element, {
  title: function () {
    // Return dynamic content
    return `Current count: ${this.dataset.count}`;
  }
});
```

---

## Technical Architecture

### System Overview

Bootstrap is a modular framework with two main components:

1. **CSS Layer** - Built with Sass (SCSS)
2. **JavaScript Layer** - Vanilla JavaScript (ES6+)

#### Architecture Diagram

```
┌─────────────────────────────────────────────────────┐
│                 Bootstrap Framework                  │
├──────────────────────┬──────────────────────────────┤
│                      │                              │
│    CSS/Sass Layer    │     JavaScript Layer         │
│                      │                              │
│  ┌────────────────┐  │  ┌─────────────────────┐    │
│  │ Variables      │  │  │ Base Component      │    │
│  │ - Colors       │  │  │ - Common methods    │    │
│  │ - Spacing      │  │  │ - Event handling    │    │
│  │ - Typography   │  │  │ - Data storage      │    │
│  └────────────────┘  │  └─────────────────────┘    │
│           │          │            │                 │
│  ┌────────────────┐  │  ┌─────────────────────┐    │
│  │ Mixins         │  │  │ DOM Utilities       │    │
│  │ - Breakpoints  │  │  │ - Event Handler     │    │
│  │ - Grid         │  │  │ - Selector Engine   │    │
│  │ - Buttons      │  │  │ - Data Management   │    │
│  └────────────────┘  │  └─────────────────────┘    │
│           │          │            │                 │
│  ┌────────────────┐  │  ┌─────────────────────┐    │
│  │ Components     │  │  │ Components          │    │
│  │ - Buttons      │  │  │ - Modal             │    │
│  │ - Cards        │  │  │ - Dropdown          │    │
│  │ - Forms        │  │  │ - Carousel          │    │
│  │ - Grid         │  │  │ - Tooltip           │    │
│  └────────────────┘  │  └─────────────────────┘    │
│           │          │            │                 │
│  ┌────────────────┐  │  ┌─────────────────────┐    │
│  │ Utilities      │  │  │ External Deps       │    │
│  │ - Display      │  │  │ - Popper.js         │    │
│  │ - Flex         │  │  │   (for positioning) │    │
│  │ - Spacing      │  │  └─────────────────────┘    │
│  └────────────────┘  │                              │
└──────────────────────┴──────────────────────────────┘
                       │
                       ▼
              ┌─────────────────┐
              │  Compiled Output │
              │  - bootstrap.css │
              │  - bootstrap.js  │
              └─────────────────┘
```

### Data Flow

#### CSS Compilation Flow

```
SCSS Source Files
      │
      ├── _variables.scss  ──→  Define base values
      │
      ├── _mixins.scss  ────→  Create reusable patterns
      │
      ├── _components.scss ──→  Build component styles
      │
      ├── _utilities.scss  ──→  Generate utility classes
      │
      ▼
   Sass Compiler
      │
      ├── Parse variables
      ├── Process mixins
      ├── Compile to CSS
      │
      ▼
   PostCSS
      │
      ├── Autoprefixer (add vendor prefixes)
      ├── RTL conversion (optional)
      │
      ▼
   Output CSS
      │
      ├── bootstrap.css
      ├── bootstrap.min.css
      ├── bootstrap.rtl.css
      └── bootstrap.rtl.min.css
```

#### JavaScript Compilation Flow

```
ES6+ Source Files
      │
      ├── base-component.js  ──→  Base class
      │
      ├── alert.js, modal.js, etc.  ──→  Components
      │
      ├── dom/  ──→  DOM utilities
      │
      ├── util/  ──→  Helper functions
      │
      ▼
   Rollup Bundler
      │
      ├── Bundle modules
      ├── Babel transpilation
      ├── Include Popper.js (for bundle version)
      │
      ▼
   Terser
      │
      ├── Minify code
      ├── Generate source maps
      │
      ▼
   Output JavaScript
      │
      ├── bootstrap.js (individual components)
      ├── bootstrap.min.js
      ├── bootstrap.bundle.js (with Popper)
      └── bootstrap.bundle.min.js
```

---

## Development Guide

### Coding Standards

#### JavaScript

**ES6+ Features:**
```javascript
// Use const/let, not var
const element = document.getElementById('myElement');
let counter = 0;

// Use arrow functions
const handleClick = (event) => {
  event.preventDefault();
};

// Use template literals
const message = `Hello, ${name}!`;

// Use destructuring
const { title, content } = modalData;

// Use default parameters
function createToast(message, type = 'info') {
  // ...
}

// Use classes
class MyComponent extends BaseComponent {
  constructor(element) {
    super(element);
  }
}
```

**Naming Conventions:**
```javascript
// Classes: PascalCase
class Modal extends BaseComponent {}

// Constants: UPPER_SNAKE_CASE
const DATA_KEY = 'bs.modal';
const EVENT_KEY = `.${DATA_KEY}`;

// Variables/Functions: camelCase
const modalElement = document.getElementById('modal');
function handleClose() {}

// Private methods: prefix with _
_queueCallback(callback, element) {}
```

**JSDoc Comments:**
```javascript
/**
 * Show the modal
 * @param {HTMLElement} relatedTarget - Element that triggered the modal
 * @returns {void}
 */
show(relatedTarget) {
  // Implementation
}
```

#### Sass/SCSS

**Variable Naming:**
```scss
// Component-state-property-size pattern
$modal-content-bg: $white;
$modal-content-border-width: $border-width;
$btn-padding-y-sm: $input-btn-padding-y-sm;
```

**Nesting Guidelines:**
```scss
// Limit nesting to 3 levels
.card {
  background-color: $card-bg;
  
  .card-body {
    padding: $card-spacer-y $card-spacer-x;
    
    .card-title {
      margin-bottom: $card-title-spacer-y;
    }
  }
}

// Use & for pseudo-classes
.btn {
  &:hover {
    background-color: $btn-hover-bg;
  }
  
  &:focus {
    outline: 0;
  }
}
```

### Testing Strategy

#### JavaScript Unit Tests

Bootstrap uses Jasmine for unit testing:

```javascript
describe('Alert', () => {
  let fixtureEl;
  
  beforeAll(() => {
    fixtureEl = getFixture();
  });
  
  afterEach(() => {
    clearFixture();
  });
  
  describe('VERSION', () => {
    it('should return plugin version', () => {
      expect(Alert.VERSION).toEqual(jasmine.any(String));
    });
  });
  
  describe('close', () => {
    it('should close an alert', () => {
      fixtureEl.innerHTML = '<div class="alert"><button class="btn-close" data-bs-dismiss="alert"></button></div>';
      
      const alertEl = fixtureEl.querySelector('.alert');
      const alert = new Alert(alertEl);
      
      alert.close();
      
      expect(alertEl).toBeNull();
    });
  });
});
```

**Run Tests:**
```bash
npm run js-test
```

#### CSS Tests

Bootstrap uses Sass True for CSS testing:

```scss
@use 'true' as *;
@use '../functions' as *;

@include describe('color-contrast') {
  @include it('should return correct contrast color') {
    @include assert-equal(
      color-contrast(#000),
      #fff,
      'Black background should have white text'
    );
  }
}
```

**Run Tests:**
```bash
npm run css-test
```

### Debugging Tips

#### JavaScript Debugging

**Enable Debug Mode:**
```javascript
// Set debug flag
bootstrap.Modal.Default.debug = true;

// Or per instance
const modal = new bootstrap.Modal(element, {
  debug: true
});
```

**Console Logging:**
```javascript
// Log component state
const modal = bootstrap.Modal.getInstance(element);
console.log('Modal config:', modal._config);
console.log('Modal element:', modal._element);
```

**Breakpoints:**
```javascript
// Add debugger statement
_handleUpdate() {
  debugger;  // Execution will pause here
  this._adjustDialog();
}
```

#### CSS Debugging

**Browser DevTools:**
```css
/* Add temporary visual debugging */
.row {
  outline: 1px solid red !important;
}

.col {
  background-color: rgba(255, 0, 0, 0.1) !important;
}
```

**Sass Debugging:**
```scss
// Use @debug directive
$primary: #0074d9;
@debug "Primary color is: #{$primary}";

// Use @warn for warnings
@if $enable-grid-classes == false {
  @warn "Grid classes are disabled!";
}
```

---

## Configuration

### Environment Variables

Bootstrap build process uses the following:

```bash
# Enable RTL build
NODE_ENV=RTL npm run css-compile

# Enable debug mode
DEBUG=true npm run js-test-karma

# Use jQuery in tests
JQUERY=true npm run js-test-karma

# Run on BrowserStack
BROWSERSTACK=true npm run js-test-karma
```

### Configuration Files

#### Sass Configuration

Override variables in your own file:

```scss
// custom.scss

// Override Bootstrap variables
$primary: #0074d9;
$secondary: #6c757d;
$border-radius: 0.5rem;
$enable-shadows: true;
$enable-gradients: false;

// Import Bootstrap
@import "bootstrap/scss/bootstrap";

// Add custom styles
.my-custom-class {
  color: $primary;
}
```

#### JavaScript Configuration

Configure via options object:

```javascript
// Global defaults
bootstrap.Modal.Default.backdrop = 'static';
bootstrap.Modal.Default.keyboard = false;

// Or per instance
const modal = new bootstrap.Modal(element, {
  backdrop: 'static',
  keyboard: false
});
```

### Feature Flags

Enable/disable features via Sass variables:

```scss
// Bootstrap feature flags
$enable-caret: true;
$enable-rounded: true;
$enable-shadows: false;
$enable-gradients: false;
$enable-transitions: true;
$enable-reduced-motion: true;
$enable-smooth-scroll: true;
$enable-grid-classes: true;
$enable-container-classes: true;
$enable-cssgrid: false;
$enable-button-pointers: true;
$enable-rfs: true;
$enable-validation-icons: true;
$enable-negative-margins: false;
$enable-deprecation-messages: true;
$enable-important-utilities: true;
$enable-dark-mode: true;
```

---

## Code Examples

### Building a Complete Component

**HTML:**
```html
<div class="card">
  <div class="card-header d-flex justify-content-between align-items-center">
    <h5 class="mb-0">User Profile</h5>
    <button class="btn btn-sm btn-primary" data-bs-toggle="modal" data-bs-target="#editModal">
      Edit
    </button>
  </div>
  <div class="card-body">
    <div class="row g-3">
      <div class="col-md-6">
        <label class="form-label">Name</label>
        <input type="text" class="form-control" value="John Doe" readonly>
      </div>
      <div class="col-md-6">
        <label class="form-label">Email</label>
        <input type="email" class="form-control" value="john@example.com" readonly>
      </div>
    </div>
  </div>
</div>

<!-- Edit Modal -->
<div class="modal fade" id="editModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Edit Profile</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <form id="editForm">
          <div class="mb-3">
            <label for="editName" class="form-label">Name</label>
            <input type="text" class="form-control" id="editName" required>
          </div>
          <div class="mb-3">
            <label for="editEmail" class="form-label">Email</label>
            <input type="email" class="form-control" id="editEmail" required>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        <button type="button" class="btn btn-primary" id="saveBtn">Save Changes</button>
      </div>
    </div>
  </div>
</div>
```

**JavaScript:**
```javascript
// Profile manager
class ProfileManager {
  constructor(formId, modalId, toastContainerId) {
    this.form = document.getElementById(formId);
    this.modal = new bootstrap.Modal(document.getElementById(modalId));
    this.toastContainer = document.getElementById(toastContainerId);
    
    this.init();
  }
  
  init() {
    // Load current data when modal opens
    document.getElementById('editModal').addEventListener('show.bs.modal', () => {
      this.loadData();
    });
    
    // Handle save
    document.getElementById('saveBtn').addEventListener('click', () => {
      this.save();
    });
  }
  
  loadData() {
    // Load current profile data
    const name = document.querySelector('[value="John Doe"]').value;
    const email = document.querySelector('[value="john@example.com"]').value;
    
    document.getElementById('editName').value = name;
    document.getElementById('editEmail').value = email;
  }
  
  async save() {
    if (!this.form.checkValidity()) {
      this.form.classList.add('was-validated');
      return;
    }
    
    const formData = {
      name: document.getElementById('editName').value,
      email: document.getElementById('editEmail').value
    };
    
    try {
      // Simulate API call
      await this.updateProfile(formData);
      
      // Update UI
      document.querySelector('[value="John Doe"]').value = formData.name;
      document.querySelector('[value="john@example.com"]').value = formData.email;
      
      // Hide modal
      this.modal.hide();
      
      // Show success toast
      this.showToast('Profile updated successfully!', 'success');
    } catch (error) {
      this.showToast('Failed to update profile', 'danger');
    }
  }
  
  async updateProfile(data) {
    // Simulate API call
    return new Promise((resolve) => {
      setTimeout(resolve, 1000);
    });
  }
  
  showToast(message, type) {
    const toastHTML = `
      <div class="toast align-items-center text-bg-${type}" role="alert">
        <div class="d-flex">
          <div class="toast-body">${message}</div>
          <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
        </div>
      </div>
    `;
    
    this.toastContainer.insertAdjacentHTML('beforeend', toastHTML);
    const toastElement = this.toastContainer.lastElementChild;
    const toast = new bootstrap.Toast(toastElement);
    toast.show();
    
    toastElement.addEventListener('hidden.bs.toast', () => {
      toastElement.remove();
    });
  }
}

// Initialize
const profileManager = new ProfileManager('editForm', 'editModal', 'toast-container');
```

---

*This developer guide provides comprehensive technical documentation for working with Bootstrap. For additional examples and detailed API documentation, visit [getbootstrap.com](https://getbootstrap.com/).*
