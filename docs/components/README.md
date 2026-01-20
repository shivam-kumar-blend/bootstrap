# Bootstrap Components Catalog

A comprehensive catalog of all Bootstrap components with descriptions, usage guidelines, and dependencies.

## Component Hierarchy and Relationships

```
Bootstrap Components
│
├── Layout Components
│   ├── Containers
│   ├── Grid System
│   └── Breakpoints
│
├── Content Components
│   ├── Typography
│   ├── Images
│   ├── Tables
│   └── Figures
│
├── Form Components
│   ├── Form Controls
│   ├── Form Select
│   ├── Form Checks & Radios
│   ├── Form Range
│   ├── Input Groups
│   ├── Floating Labels
│   └── Form Validation
│
├── UI Components (CSS Only)
│   ├── Alerts
│   ├── Badges
│   ├── Breadcrumbs
│   ├── Buttons
│   ├── Button Groups
│   ├── Cards
│   ├── List Groups
│   ├── Pagination
│   ├── Progress Bars
│   └── Spinners
│
├── UI Components (JavaScript Required)
│   ├── Accordion
│   ├── Carousel
│   ├── Collapse
│   ├── Dropdowns
│   ├── Modals
│   ├── Offcanvas
│   ├── Popovers
│   ├── Scrollspy
│   ├── Tabs
│   ├── Toasts
│   └── Tooltips
│
├── Navigation Components
│   ├── Navbar
│   ├── Navs & Tabs
│   └── Breadcrumb
│
└── Utility Components
    ├── Close Button
    ├── Placeholders
    └── Toasts
```

---

## Layout Components

### Containers

**Description**: Responsive containers that wrap content and provide proper padding and alignment.

**Types**:
- `.container` - Fixed-width responsive container
- `.container-fluid` - Full-width container
- `.container-{breakpoint}` - 100% wide until specified breakpoint

**Dependencies**: None

**Use Cases**:
- Wrapping page content
- Creating centered layouts
- Responsive width management

**Example**:
```html
<div class="container">
  <!-- Content -->
</div>
```

---

### Grid System

**Description**: Powerful 12-column responsive grid system built with flexbox.

**Classes**:
- `.row` - Grid row
- `.col`, `.col-*` - Equal width columns
- `.col-{breakpoint}-{number}` - Responsive column sizes
- `.g-*`, `.gx-*`, `.gy-*` - Gutter spacing

**Dependencies**: None

**Use Cases**:
- Creating responsive layouts
- Multi-column designs
- Complex page structures

**Example**:
```html
<div class="container">
  <div class="row">
    <div class="col-md-8">Main content</div>
    <div class="col-md-4">Sidebar</div>
  </div>
</div>
```

---

## Content Components

### Typography

**Description**: Styles for headings, paragraphs, lists, and text formatting.

**Classes**:
- `.h1` - `.h6` - Heading styles
- `.display-1` - `.display-6` - Large display headings
- `.lead` - Stand-out paragraph
- `.text-*` - Text utilities (alignment, color, etc.)

**Dependencies**: None

**Example**:
```html
<h1 class="display-4">Large Heading</h1>
<p class="lead">This is a lead paragraph.</p>
```

---

### Tables

**Description**: Enhanced table styles with optional modifiers.

**Classes**:
- `.table` - Base table styles
- `.table-striped` - Zebra striping
- `.table-hover` - Hover state
- `.table-bordered` - Borders on all sides
- `.table-responsive` - Horizontal scrolling

**Dependencies**: None

**Use Cases**:
- Displaying tabular data
- Data tables
- Price comparisons

**Example**:
```html
<table class="table table-striped table-hover">
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>John Doe</td>
      <td>john@example.com</td>
    </tr>
  </tbody>
</table>
```

---

## Form Components

### Form Controls

**Description**: Styled text inputs, textareas, and select menus.

**Classes**:
- `.form-control` - Text inputs and textareas
- `.form-control-lg` / `.form-control-sm` - Size variants
- `.form-label` - Form labels
- `.form-text` - Helper text

**Dependencies**: None

**Use Cases**:
- Contact forms
- Login/registration forms
- Data entry forms

**Example**:
```html
<div class="mb-3">
  <label for="email" class="form-label">Email</label>
  <input type="email" class="form-control" id="email">
  <div class="form-text">We'll never share your email.</div>
</div>
```

---

### Form Validation

**Description**: Client-side validation styles and feedback.

**Classes**:
- `.needs-validation` - Form needing validation
- `.was-validated` - Form that has been validated
- `.is-valid` / `.is-invalid` - Validation states
- `.valid-feedback` / `.invalid-feedback` - Feedback messages

**Dependencies**: JavaScript (for validation logic)

**Use Cases**:
- Form validation
- User input verification
- Error messaging

**Example**:
```html
<form class="needs-validation" novalidate>
  <div class="mb-3">
    <label for="username" class="form-label">Username</label>
    <input type="text" class="form-control" id="username" required>
    <div class="invalid-feedback">Please choose a username.</div>
  </div>
</form>
```

---

### Floating Labels

**Description**: Material Design-style floating form labels.

**Classes**:
- `.form-floating` - Container for floating label

**Dependencies**: None

**Use Cases**:
- Modern form design
- Space-efficient forms
- Material Design aesthetic

**Example**:
```html
<div class="form-floating mb-3">
  <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
  <label for="floatingInput">Email address</label>
</div>
```

---

## UI Components (CSS Only)

### Alerts

**Description**: Contextual feedback messages for user actions.

**Classes**:
- `.alert` - Base alert
- `.alert-{variant}` - Color variants (primary, success, danger, etc.)
- `.alert-dismissible` - Dismissible alert
- `.alert-link` - Matching links

**Dependencies**: 
- CSS: None
- JavaScript: Optional (for dismiss functionality)

**Use Cases**:
- Success messages
- Error notifications
- Warning messages
- Info banners

**Example**:
```html
<div class="alert alert-success alert-dismissible fade show" role="alert">
  <strong>Success!</strong> Your changes have been saved.
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

### Badges

**Description**: Small count and labeling components.

**Classes**:
- `.badge` - Base badge
- `.badge-{variant}` - Color variants
- `.rounded-pill` - Pill-shaped badges

**Dependencies**: None

**Use Cases**:
- Notification counts
- Status labels
- Tags and categories

**Example**:
```html
<button type="button" class="btn btn-primary">
  Notifications <span class="badge bg-secondary">4</span>
</button>
```

---

### Buttons

**Description**: Custom button styles for actions and navigation.

**Classes**:
- `.btn` - Base button
- `.btn-{variant}` - Color variants
- `.btn-{size}` - Size variants (lg, sm)
- `.btn-outline-{variant}` - Outline buttons
- `.btn-group` - Button groups

**Dependencies**: None (JavaScript optional for toggle states)

**Use Cases**:
- Form submissions
- Call-to-action buttons
- Navigation elements
- Toolbars

**Example**:
```html
<button type="button" class="btn btn-primary">Primary</button>
<button type="button" class="btn btn-outline-secondary">Secondary</button>
```

---

### Cards

**Description**: Flexible content containers with multiple variants.

**Classes**:
- `.card` - Base card
- `.card-header` / `.card-body` / `.card-footer` - Card sections
- `.card-img-top` / `.card-img-bottom` - Images
- `.card-title` / `.card-text` - Typography

**Dependencies**: None

**Use Cases**:
- Product listings
- Blog post previews
- User profiles
- Dashboard widgets

**Example**:
```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

---

### Progress Bars

**Description**: Progress indicators for workflows and loading states.

**Classes**:
- `.progress` - Progress container
- `.progress-bar` - Progress indicator
- `.progress-bar-striped` - Striped variant
- `.progress-bar-animated` - Animated stripes

**Dependencies**: None

**Use Cases**:
- Upload progress
- Multi-step forms
- Loading indicators
- Skill meters

**Example**:
```html
<div class="progress">
  <div class="progress-bar" role="progressbar" style="width: 75%" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">75%</div>
</div>
```

---

### Spinners

**Description**: Loading spinners in multiple sizes and styles.

**Classes**:
- `.spinner-border` - Border spinner
- `.spinner-grow` - Growing spinner
- `.spinner-border-sm` / `.spinner-grow-sm` - Small sizes

**Dependencies**: None

**Use Cases**:
- Loading states
- Async operations
- Button loading states

**Example**:
```html
<div class="spinner-border text-primary" role="status">
  <span class="visually-hidden">Loading...</span>
</div>
```

---

## UI Components (JavaScript Required)

### Accordion

**Description**: Vertically collapsing panels for organizing content.

**Classes**:
- `.accordion` - Container
- `.accordion-item` - Individual item
- `.accordion-header` - Header
- `.accordion-collapse` - Collapsible content
- `.accordion-body` - Body content

**Dependencies**: 
- JavaScript: `collapse.js`
- External: None

**Context Requirements**: None

**Use Cases**:
- FAQs
- Product details
- Content organization
- Vertical navigation

**Example**:
```html
<div class="accordion" id="accordionExample">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne">
        Accordion Item #1
      </button>
    </h2>
    <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
      <div class="accordion-body">
        Content goes here.
      </div>
    </div>
  </div>
</div>
```

---

### Carousel

**Description**: Slideshow component for cycling through elements.

**Classes**:
- `.carousel` - Container
- `.carousel-inner` - Slides container
- `.carousel-item` - Individual slide
- `.carousel-control-prev/next` - Navigation controls
- `.carousel-indicators` - Position indicators

**Dependencies**: 
- JavaScript: `carousel.js`
- External: None

**Context Requirements**: None

**Use Cases**:
- Image galleries
- Product showcases
- Hero sliders
- Testimonials

**Example**:
```html
<div id="carouselExample" class="carousel slide" data-bs-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="..." class="d-block w-100" alt="...">
    </div>
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
    <span class="carousel-control-prev-icon"></span>
  </button>
</div>
```

---

### Modal

**Description**: Dialog overlays for focused content and actions.

**Classes**:
- `.modal` - Modal container
- `.modal-dialog` - Modal dialog
- `.modal-content` - Content wrapper
- `.modal-header/body/footer` - Modal sections
- `.modal-{size}` - Size variants

**Dependencies**: 
- JavaScript: `modal.js`, `backdrop.js`, `focustrap.js`, `scrollbar.js`
- External: None

**Context Requirements**: None

**Use Cases**:
- Confirmation dialogs
- Forms
- Image lightboxes
- Alerts requiring attention

**Example**:
```html
<div class="modal fade" id="exampleModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Modal title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <p>Modal body text goes here.</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
```

---

### Dropdowns

**Description**: Toggleable contextual overlays for links and actions.

**Classes**:
- `.dropdown` - Dropdown container
- `.dropdown-toggle` - Toggle button
- `.dropdown-menu` - Menu
- `.dropdown-item` - Menu items
- `.dropdown-divider` - Dividers

**Dependencies**: 
- JavaScript: `dropdown.js`
- External: Popper.js

**Context Requirements**: None

**Use Cases**:
- Action menus
- User account menus
- Filter options
- Navigation

**Example**:
```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown">
    Dropdown button
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
  </ul>
</div>
```

---

### Tooltips

**Description**: Small pop-up boxes that appear on hover.

**Classes**:
- Applied via JavaScript initialization
- Content set via `title` attribute or `data-bs-title`

**Dependencies**: 
- JavaScript: `tooltip.js`
- External: Popper.js

**Context Requirements**: None

**Initialization Required**: Yes

```javascript
const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
const tooltipList = [...tooltipTriggerList].map(tooltipTriggerEl => new bootstrap.Tooltip(tooltipTriggerEl));
```

**Use Cases**:
- Help text
- Additional information
- Icon explanations

**Example**:
```html
<button type="button" class="btn btn-secondary" 
        data-bs-toggle="tooltip" 
        data-bs-placement="top"
        data-bs-title="Tooltip on top">
  Hover me
</button>
```

---

### Toasts

**Description**: Lightweight notifications designed to mimic push notifications.

**Classes**:
- `.toast` - Toast container
- `.toast-header` - Header
- `.toast-body` - Body content

**Dependencies**: 
- JavaScript: `toast.js`
- External: None

**Context Requirements**: None

**Use Cases**:
- Success notifications
- Error messages
- System notifications
- Undo actions

**Example**:
```html
<div class="toast" role="alert">
  <div class="toast-header">
    <strong class="me-auto">Bootstrap</strong>
    <small>11 mins ago</small>
    <button type="button" class="btn-close" data-bs-dismiss="toast"></button>
  </div>
  <div class="toast-body">
    Hello, world! This is a toast message.
  </div>
</div>
```

---

## Navigation Components

### Navbar

**Description**: Responsive navigation header with support for branding, navigation, and more.

**Classes**:
- `.navbar` - Navbar container
- `.navbar-brand` - Brand/logo
- `.navbar-nav` - Navigation links
- `.navbar-toggler` - Mobile toggle
- `.navbar-expand-{breakpoint}` - Responsive behavior

**Dependencies**: 
- JavaScript: Optional (for collapse behavior)
- External: None

**Use Cases**:
- Site headers
- Application navigation
- Mobile menus

**Example**:
```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

---

## Design System Tokens

### Colors

Bootstrap provides a comprehensive color palette:

**Theme Colors**:
- Primary: `$primary` (#0d6efd)
- Secondary: `$secondary` (#6c757d)
- Success: `$success` (#198754)
- Danger: `$danger` (#dc3545)
- Warning: `$warning` (#ffc107)
- Info: `$info` (#0dcaf0)
- Light: `$light` (#f8f9fa)
- Dark: `$dark` (#212529)

**Grayscale**:
- Gray-100 through Gray-900
- White and Black

---

### Spacing

Bootstrap uses a consistent spacing scale:

```
0 = 0
1 = $spacer * 0.25    (0.25rem = 4px)
2 = $spacer * 0.5     (0.5rem = 8px)
3 = $spacer * 1       (1rem = 16px)
4 = $spacer * 1.5     (1.5rem = 24px)
5 = $spacer * 3       (3rem = 48px)
```

**Usage**:
- `m-*` - Margin
- `p-*` - Padding
- `mt-*, mb-*, ms-*, me-*` - Margin sides
- `pt-*, pb-*, ps-*, pe-*` - Padding sides

---

### Typography

**Font Family**:
- Default: System font stack
- Monospace: Available for code

**Font Sizes**:
- Base: 1rem (16px)
- Headings: 2.5rem - 0.875rem
- Display: 5rem - 2.5rem

**Line Height**:
- Base: 1.5
- Headings: 1.2
- Large: 2

---

### Breakpoints

Bootstrap uses 6 responsive breakpoints:

```
xs: < 576px
sm: ≥ 576px
md: ≥ 768px
lg: ≥ 992px
xl: ≥ 1200px
xxl: ≥ 1400px
```

---

## Component Dependencies Summary

### No Dependencies (CSS Only)
- Containers
- Grid
- Typography
- Tables
- Alerts (static)
- Badges
- Breadcrumbs
- Buttons (static)
- Cards
- List Groups
- Pagination
- Progress Bars
- Spinners

### JavaScript Only
- Carousel
- Collapse/Accordion
- Modal
- Offcanvas
- Scrollspy
- Tabs
- Toast

### JavaScript + Popper.js
- Dropdown
- Popover
- Tooltip

---

## Accessibility Considerations

All Bootstrap components follow WCAG 2.1 Level AA guidelines:

- **Keyboard Navigation**: All interactive components
- **ARIA Attributes**: Proper role and state attributes
- **Focus Management**: Visible focus indicators, focus trapping for modals
- **Color Contrast**: Minimum 4.5:1 for normal text
- **Screen Reader Support**: Hidden labels, live regions

---

*This component catalog provides a comprehensive overview of all Bootstrap components. For detailed usage and API documentation, see the individual component guides and the Developer Guide.*
