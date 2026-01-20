# Bootstrap Design System

A comprehensive guide to Bootstrap's design system, including design tokens, patterns, and guidelines.

## Introduction

Bootstrap's design system provides a cohesive set of design standards, components, and guidelines that ensure consistency across all projects. This document serves as the single source of truth for designers and developers working with Bootstrap.

---

## Design Tokens

Design tokens are the visual design atoms of the design system—specifically, they are named entities that store visual design attributes.

### Color Palette

#### Theme Colors

Bootstrap's theme colors form the foundation of the color system:

```scss
// Primary brand colors
$primary:   #0d6efd;  // Primary blue
$secondary: #6c757d;  // Gray
$success:   #198754;  // Green
$danger:    #dc3545;  // Red
$warning:   #ffc107;  // Yellow
$info:      #0dcaf0;  // Cyan
$light:     #f8f9fa;  // Light gray
$dark:      #212529;  // Dark gray
```

**Usage Guidelines**:
- **Primary**: Main actions, links, active states
- **Secondary**: Less prominent actions
- **Success**: Successful operations, confirmations
- **Danger**: Destructive actions, errors
- **Warning**: Warnings, cautions
- **Info**: Informational messages
- **Light**: Light backgrounds, subtle borders
- **Dark**: Dark backgrounds, primary text

#### Grayscale

```scss
$white:    #fff;
$gray-100: #f8f9fa;  // Lightest
$gray-200: #e9ecef;
$gray-300: #dee2e6;
$gray-400: #ced4da;
$gray-500: #adb5bd;  // Medium
$gray-600: #6c757d;
$gray-700: #495057;
$gray-800: #343a40;
$gray-900: #212529;  // Darkest
$black:    #000;
```

**Usage Guidelines**:
- **100-300**: Backgrounds, borders, subtle UI elements
- **400-600**: Disabled states, placeholders, secondary text
- **700-900**: Primary text, headings, active elements

#### Color Utilities

Bootstrap generates utility classes for all theme colors:

```html
<!-- Background colors -->
<div class="bg-primary">Primary background</div>
<div class="bg-success">Success background</div>

<!-- Text colors -->
<p class="text-danger">Danger text</p>
<p class="text-muted">Muted text</p>

<!-- Border colors -->
<div class="border border-warning">Warning border</div>
```

#### Color Tints and Shades

Each color has tints (mixed with white) and shades (mixed with black):

```scss
// Example: Primary color variations
$blue-100: tint-color($blue, 80%);  // Lightest
$blue-200: tint-color($blue, 60%);
$blue-300: tint-color($blue, 40%);
$blue-400: tint-color($blue, 20%);
$blue-500: $blue;                   // Base color
$blue-600: shade-color($blue, 20%);
$blue-700: shade-color($blue, 40%);
$blue-800: shade-color($blue, 60%);
$blue-900: shade-color($blue, 80%); // Darkest
```

#### Accessibility: Color Contrast

Bootstrap ensures WCAG 2.1 Level AA compliance:

```scss
// Minimum contrast ratio
$min-contrast-ratio: 4.5;

// Automatically calculated contrasting text colors
$color-contrast-dark:  $black;   // For light backgrounds
$color-contrast-light: $white;   // For dark backgrounds
```

**Testing**: Use the `color-contrast()` Sass function to ensure proper contrast:

```scss
.my-component {
  background-color: $primary;
  color: color-contrast($primary);  // Automatically white or black
}
```

---

### Typography

#### Font Families

```scss
// System font stack for performance
$font-family-sans-serif: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", 
                         "Noto Sans", "Liberation Sans", Arial, sans-serif;

// Monospace for code
$font-family-monospace: SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", 
                        "Courier New", monospace;

// Base font family
$font-family-base: $font-family-sans-serif;
```

**Usage Guidelines**:
- Use system fonts for fast loading and native feel
- Use monospace only for code, pre-formatted text
- Override `$font-family-base` to use custom fonts

#### Font Sizes

```scss
// Base font size
$font-size-base: 1rem;  // 16px

// Font size scale
$font-size-sm: $font-size-base * 0.875;  // 14px
$font-size-lg: $font-size-base * 1.25;   // 20px

// Heading sizes
$h1-font-size: $font-size-base * 2.5;    // 40px
$h2-font-size: $font-size-base * 2;      // 32px
$h3-font-size: $font-size-base * 1.75;   // 28px
$h4-font-size: $font-size-base * 1.5;    // 24px
$h5-font-size: $font-size-base * 1.25;   // 20px
$h6-font-size: $font-size-base;          // 16px

// Display sizes (larger than headings)
$display-font-sizes: (
  1: 5rem,      // 80px
  2: 4.5rem,    // 72px
  3: 4rem,      // 64px
  4: 3.5rem,    // 56px
  5: 3rem,      // 48px
  6: 2.5rem     // 40px
);
```

**Hierarchy**:
```
Display 1-6  → Hero/Landing pages
H1          → Page title
H2          → Major sections
H3          → Subsections
H4-H6       → Minor headings
Body (base) → Body text
Small       → Captions, footnotes
```

#### Line Heights

```scss
$line-height-base: 1.5;      // Body text
$line-height-sm: 1.25;       // Compact text
$line-height-lg: 2;          // Relaxed text

// Headings use a tighter line height
$headings-line-height: 1.2;
```

**Usage**:
- **1.5**: Default for body text (optimal readability)
- **1.25**: Compact lists, small text
- **2**: Lead paragraphs, relaxed reading
- **1.2**: Headings (prevents excessive space)

#### Font Weights

```scss
$font-weight-lighter: lighter;  // Relative lighter
$font-weight-light: 300;        // Light
$font-weight-normal: 400;       // Normal/Regular
$font-weight-semibold: 600;     // Semi-bold
$font-weight-bold: 700;         // Bold
$font-weight-bolder: bolder;    // Relative bolder
```

**Typography Utilities**:
```html
<p class="fw-light">Light text</p>
<p class="fw-normal">Normal text</p>
<p class="fw-bold">Bold text</p>
<p class="fst-italic">Italic text</p>
<p class="text-decoration-underline">Underlined text</p>
```

---

### Spacing System

Bootstrap uses a consistent spacing scale based on a base unit (`$spacer`):

```scss
$spacer: 1rem;  // 16px

// Spacing scale
$spacers: (
  0: 0,                    // 0px
  1: $spacer * 0.25,       // 4px
  2: $spacer * 0.5,        // 8px
  3: $spacer,              // 16px
  4: $spacer * 1.5,        // 24px
  5: $spacer * 3,          // 48px
);
```

#### Spacing Utilities

**Margin**: `m{sides}-{size}`  
**Padding**: `p{sides}-{size}`

**Sides**:
- `t` - Top
- `b` - Bottom
- `s` - Start (left in LTR, right in RTL)
- `e` - End (right in LTR, left in RTL)
- `x` - Horizontal (left and right)
- `y` - Vertical (top and bottom)
- (blank) - All sides

**Examples**:
```html
<div class="mt-3">Margin top 1rem</div>
<div class="px-4">Padding left/right 1.5rem</div>
<div class="mb-5">Margin bottom 3rem</div>
<div class="m-0">No margin</div>
<div class="mx-auto">Centered with auto margin</div>
```

#### Responsive Spacing

Add breakpoint infix for responsive spacing:

```html
<div class="mt-2 mt-md-4 mt-lg-5">
  <!-- Margin top: 8px on mobile, 24px on tablet, 48px on desktop -->
</div>
```

---

### Borders

#### Border Width

```scss
$border-width: 1px;
$border-widths: (
  1: 1px,
  2: 2px,
  3: 3px,
  4: 4px,
  5: 5px
);
```

#### Border Radius

```scss
$border-radius:    0.375rem;  // 6px - Default
$border-radius-sm: 0.25rem;   // 4px - Small
$border-radius-lg: 0.5rem;    // 8px - Large
$border-radius-xl: 1rem;      // 16px - Extra large
$border-radius-2xl: 2rem;     // 32px - 2X Extra large
$border-radius-pill: 50rem;   // Pill shape
```

**Border Utilities**:
```html
<!-- Add borders -->
<div class="border">All sides</div>
<div class="border-top">Top only</div>

<!-- Border colors -->
<div class="border border-primary">Primary border</div>

<!-- Border radius -->
<div class="rounded">Default radius</div>
<div class="rounded-circle">Circle</div>
<div class="rounded-pill">Pill</div>

<!-- Border width -->
<div class="border border-3">3px border</div>
```

---

### Shadows

```scss
// Box shadow levels
$box-shadow:    0 0.5rem 1rem rgba($black, 0.15);
$box-shadow-sm: 0 0.125rem 0.25rem rgba($black, 0.075);
$box-shadow-lg: 0 1rem 3rem rgba($black, 0.175);
$box-shadow-inset: inset 0 1px 2px rgba($black, 0.075);
```

**Shadow Utilities**:
```html
<div class="shadow-sm">Small shadow</div>
<div class="shadow">Default shadow</div>
<div class="shadow-lg">Large shadow</div>
<div class="shadow-none">No shadow</div>
```

**Usage**:
- **sm**: Subtle elevation (cards, inputs)
- **default**: Medium elevation (dropdowns, tooltips)
- **lg**: High elevation (modals, popovers)

---

### Breakpoints

Bootstrap's responsive breakpoint system:

```scss
$grid-breakpoints: (
  xs: 0,        // Extra small (phones)
  sm: 576px,    // Small (landscape phones)
  md: 768px,    // Medium (tablets)
  lg: 992px,    // Large (desktops)
  xl: 1200px,   // Extra large (large desktops)
  xxl: 1400px   // Extra extra large (larger desktops)
);
```

#### Container Max Widths

```scss
$container-max-widths: (
  sm: 540px,
  md: 720px,
  lg: 960px,
  xl: 1140px,
  xxl: 1320px
);
```

**Responsive Design Philosophy**:
1. **Mobile First**: Design for smallest screen first
2. **Progressive Enhancement**: Add features for larger screens
3. **Fluid Typography**: Use `rem` units for scalability
4. **Flexible Images**: Images scale with containers

---

## Component Patterns

### Button Patterns

**Standard Button Hierarchy**:

```html
<!-- Primary action (one per view) -->
<button class="btn btn-primary">Save Changes</button>

<!-- Secondary actions -->
<button class="btn btn-secondary">Cancel</button>
<button class="btn btn-outline-primary">Learn More</button>

<!-- Destructive actions -->
<button class="btn btn-danger">Delete</button>

<!-- Disabled state -->
<button class="btn btn-primary" disabled>Processing...</button>
```

**Button Sizing**:
- Large: Main CTAs, hero sections
- Default: Most buttons
- Small: Compact UIs, secondary actions

**Best Practices**:
- Use one primary button per view
- Place primary button on the right (in Western locales)
- Use outline buttons for secondary actions
- Always provide visual and textual feedback for loading states

---

### Form Patterns

**Form Layout Patterns**:

```html
<!-- Vertical Form (Default) -->
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input type="email" class="form-control" id="email">
  </div>
</form>

<!-- Horizontal Form -->
<form>
  <div class="row mb-3">
    <label for="email" class="col-sm-2 col-form-label">Email</label>
    <div class="col-sm-10">
      <input type="email" class="form-control" id="email">
    </div>
  </div>
</form>

<!-- Inline Form -->
<form class="row row-cols-auto g-3 align-items-center">
  <div class="col">
    <input type="text" class="form-control" placeholder="Username">
  </div>
  <div class="col">
    <button type="submit" class="btn btn-primary">Submit</button>
  </div>
</form>
```

**Form Validation Pattern**:
1. Validate on blur for long forms
2. Validate on submit for short forms
3. Show success state after correction
4. Provide specific error messages
5. Use icons to reinforce state

---

### Card Patterns

**Card Layouts**:

```html
<!-- Information Card -->
<div class="card">
  <div class="card-body">
    <h5 class="card-title">Title</h5>
    <p class="card-text">Content</p>
  </div>
</div>

<!-- Image Card -->
<div class="card">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Title</h5>
    <p class="card-text">Content</p>
    <a href="#" class="btn btn-primary">Action</a>
  </div>
</div>

<!-- Card with Header and Footer -->
<div class="card">
  <div class="card-header">Featured</div>
  <div class="card-body">
    <h5 class="card-title">Title</h5>
    <p class="card-text">Content</p>
  </div>
  <div class="card-footer text-muted">2 days ago</div>
</div>
```

**Card Grids**:
```html
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
  <div class="col">
    <div class="card h-100"><!-- Card content --></div>
  </div>
  <!-- Repeat -->
</div>
```

---

### Navigation Patterns

**Navbar Pattern**:

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <!-- Brand -->
    <a class="navbar-brand" href="#">
      <img src="logo.svg" alt="Logo" height="30">
    </a>
    
    <!-- Mobile toggle -->
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    
    <!-- Navigation -->
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Features</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

---

### Modal Patterns

**Standard Modal Pattern**:

```html
<div class="modal fade" id="exampleModal" tabindex="-1">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Modal Title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        Content goes here
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        <button type="button" class="btn btn-primary">Confirm</button>
      </div>
    </div>
  </div>
</div>
```

**Modal Sizes**:
- Small: Simple confirmations
- Default: Forms, content
- Large: Complex forms, tables
- Extra large: Rich content
- Fullscreen: Immersive experiences

---

## Layout Guidelines

### Grid Best Practices

1. **Always use containers**:
   ```html
   <div class="container">
     <div class="row">
       <div class="col">Content</div>
     </div>
   </div>
   ```

2. **Columns must be direct children of rows**:
   ```html
   <!-- ✓ Correct -->
   <div class="row">
     <div class="col">Content</div>
   </div>
   
   <!-- ✗ Wrong -->
   <div class="row">
     <div>
       <div class="col">Content</div>
     </div>
   </div>
   ```

3. **Use gutters appropriately**:
   ```html
   <!-- Default gutters -->
   <div class="row">
     <div class="col">Column</div>
   </div>
   
   <!-- No gutters -->
   <div class="row g-0">
     <div class="col">Column</div>
   </div>
   
   <!-- Custom gutters -->
   <div class="row g-4">
     <div class="col">Column</div>
   </div>
   ```

---

## Accessibility Guidelines

### WCAG 2.1 Level AA Compliance

Bootstrap is designed to meet WCAG 2.1 Level AA standards:

#### Color Contrast
- **Normal text**: Minimum 4.5:1 contrast ratio
- **Large text**: Minimum 3:1 contrast ratio
- **UI components**: Minimum 3:1 contrast ratio

#### Keyboard Navigation
All interactive components must be:
- Focusable via keyboard
- Activatable via Enter or Space
- Navigable via arrow keys (where applicable)

#### Screen Reader Support
- Use semantic HTML elements
- Provide ARIA labels where needed
- Use `aria-hidden` for decorative elements
- Provide alternative text for images

#### Focus Management
- Visible focus indicators
- Logical focus order
- Focus trap in modals
- Focus restoration after modals close

**Example: Accessible Button**:
```html
<button type="button" class="btn btn-primary" aria-label="Save document">
  <i class="bi bi-save" aria-hidden="true"></i>
  Save
</button>
```

---

## Animation Guidelines

### Transition Durations

```scss
$transition-base: all 0.2s ease-in-out;
$transition-fade: opacity 0.15s linear;
$transition-collapse: height 0.35s ease;
```

**Usage**:
- **0.15s**: Fast transitions (fades, color changes)
- **0.2s**: Standard transitions (buttons, links)
- **0.35s**: Slow transitions (collapse, modal)

### Reduced Motion

Respect user preferences:

```scss
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Icon Guidelines

Bootstrap does not include an icon library, but works well with:

**Recommended Icon Libraries**:
- **Bootstrap Icons**: Official icon library
- **Font Awesome**: Popular icon set
- **Material Icons**: Google's icon set
- **Feather Icons**: Minimal, beautiful icons

**Usage with Bootstrap**:
```html
<!-- Bootstrap Icons -->
<i class="bi bi-heart-fill text-danger"></i>

<!-- With buttons -->
<button class="btn btn-primary">
  <i class="bi bi-download"></i> Download
</button>
```

---

## Dark Mode

Bootstrap 5.3+ includes built-in dark mode support:

```html
<!-- Enable dark mode -->
<html data-bs-theme="dark">

<!-- Auto (respects system preference) -->
<html data-bs-theme="auto">

<!-- Light mode (default) -->
<html data-bs-theme="light">
```

**Customizing Dark Mode Colors**:
```scss
// Dark mode variables
$primary-dark: #6ea8fe;
$secondary-dark: #6c757d;
$body-bg-dark: #212529;
$body-color-dark: #dee2e6;
```

---

*This design system documentation provides comprehensive guidelines for using Bootstrap's visual design language. For component-specific details, see the Components Catalog.*
