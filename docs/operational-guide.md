# Bootstrap Operational Guide

This guide covers deployment, monitoring, troubleshooting, maintenance, and operational best practices for Bootstrap.

## Deployment Procedures

### Deploying Bootstrap to Production

#### Option 1: CDN Deployment (Recommended for Most Users)

The simplest deployment method is using a CDN:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" 
        rel="stylesheet" 
        integrity="sha384-..." 
        crossorigin="anonymous">
</head>
<body>
  <!-- Your content -->
  
  <!-- Bootstrap Bundle with Popper -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" 
          integrity="sha384-..." 
          crossorigin="anonymous"></script>
</body>
</html>
```

**Advantages:**
- Fast global delivery
- Automatic caching
- No build process needed
- Reduced server load

**CDN Providers:**
- jsDelivr (recommended)
- cdnjs
- unpkg

#### Option 2: Self-Hosted Deployment

For projects requiring full control:

1. **Build Bootstrap:**
   ```bash
   npm install bootstrap@5.3.8
   npm run dist
   ```

2. **Copy Distribution Files:**
   ```bash
   # Copy CSS
   cp dist/css/bootstrap.min.css public/css/
   cp dist/css/bootstrap.min.css.map public/css/
   
   # Copy JavaScript
   cp dist/js/bootstrap.bundle.min.js public/js/
   cp dist/js/bootstrap.bundle.min.js.map public/js/
   ```

3. **Reference in HTML:**
   ```html
   <link href="/css/bootstrap.min.css" rel="stylesheet">
   <script src="/js/bootstrap.bundle.min.js"></script>
   ```

#### Option 3: Build System Integration

For custom builds with bundlers:

**Webpack Configuration:**
```javascript
// webpack.config.js
module.exports = {
  entry: './src/index.js',
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      }
    ]
  }
};
```

**Import in JavaScript:**
```javascript
// Import all Bootstrap
import 'bootstrap';
import 'bootstrap/scss/bootstrap.scss';

// Or import only what you need
import { Modal, Dropdown } from 'bootstrap';
import 'bootstrap/scss/modal';
import 'bootstrap/scss/dropdown';
```

**Vite Configuration:**
```javascript
// vite.config.js
import { defineConfig } from 'vite';

export default defineConfig({
  css: {
    preprocessorOptions: {
      scss: {
        additionalData: `@import "bootstrap/scss/functions";`
      }
    }
  }
});
```

### Release Deployment Steps

When deploying a new version of Bootstrap:

1. **Run Full Test Suite:**
   ```bash
   npm test
   ```

2. **Build Distribution Files:**
   ```bash
   npm run dist
   ```

3. **Generate Subresource Integrity (SRI) Hashes:**
   ```bash
   npm run release-sri
   ```

4. **Build Documentation:**
   ```bash
   npm run docs-build
   ```

5. **Create Release Archive:**
   ```bash
   npm run release-zip
   ```

6. **Tag Release:**
   ```bash
   git tag -a v5.3.8 -m "Release v5.3.8"
   git push origin v5.3.8
   ```

7. **Publish to npm:**
   ```bash
   npm publish
   ```

8. **Deploy Documentation:**
   ```bash
   # Documentation is auto-deployed via Netlify on merge to main
   ```

---

## Monitoring and Alerting Setup

### Performance Monitoring

#### Bundle Size Monitoring

Bootstrap uses BundleWatch for tracking bundle sizes:

```json
{
  "files": [
    {
      "path": "dist/css/bootstrap.min.css",
      "maxSize": "25 kB"
    },
    {
      "path": "dist/js/bootstrap.bundle.min.js",
      "maxSize": "30 kB"
    }
  ]
}
```

**Run BundleWatch:**
```bash
npm run bundlewatch
```

**CI/CD Integration:**
BundleWatch runs automatically on every commit via GitHub Actions.

#### Browser Compatibility Monitoring

Bootstrap uses BrowserStack for cross-browser testing:

```bash
# Run tests on BrowserStack
npm run js-test-cloud
```

**Monitored Browsers:**
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile Safari (iOS)
- Chrome Mobile (Android)

### Security Monitoring

#### Dependency Vulnerability Scanning

Bootstrap uses several tools for security monitoring:

1. **GitHub Dependabot:**
   - Automatically scans dependencies
   - Creates PRs for security updates
   - Configured in `.github/dependabot.yml`

2. **npm audit:**
   ```bash
   npm audit
   npm audit fix
   ```

3. **Lockfile Linting:**
   ```bash
   npm run lockfile-lint
   ```

#### Code Security Scanning

**CodeQL Analysis:**
- Runs on every push and PR
- Scans for common vulnerabilities
- Configuration: `.github/workflows/codeql.yml`

**OpenSSF Scorecard:**
- Evaluates security practices
- Publicly visible score
- Badge in README

### Quality Monitoring

#### Code Coverage

Bootstrap uses Istanbul for code coverage:

```bash
# Run with coverage
npm run js-test-karma

# Coverage reports in coverage/ directory
```

**Coverage Thresholds:**
- Statements: > 90%
- Branches: > 85%
- Functions: > 90%
- Lines: > 90%

#### Linting and Code Quality

**ESLint (JavaScript):**
```bash
npm run js-lint
```

**Stylelint (CSS/Sass):**
```bash
npm run css-lint
```

**Spell Checking:**
```bash
npm run cspell
```

---

## Troubleshooting Common Issues

### Build Issues

#### Issue: Sass Compilation Fails

**Symptoms:**
```
Error: Invalid CSS after "...": expected "}", was "..."
```

**Solutions:**

1. **Check Sass Version:**
   ```bash
   npm list sass
   # Should be 1.78.0
   ```

2. **Clear Cache:**
   ```bash
   rm -rf node_modules/.cache
   npm run css-compile
   ```

3. **Verify Variable Overrides:**
   ```scss
   // Variables must be set BEFORE importing Bootstrap
   $primary: #0074d9;
   @import "bootstrap/scss/bootstrap";
   ```

#### Issue: JavaScript Build Fails

**Symptoms:**
```
RollupError: Could not resolve entry module
```

**Solutions:**

1. **Clean and Rebuild:**
   ```bash
   rm -rf dist/js
   npm run js-compile
   ```

2. **Check for Syntax Errors:**
   ```bash
   npm run js-lint
   ```

3. **Verify Dependencies:**
   ```bash
   npm install
   ```

### Runtime Issues

#### Issue: Modal Not Opening

**Symptoms:** Modal button clicked but nothing happens.

**Diagnostics:**
```javascript
// Check if Bootstrap is loaded
console.log(typeof bootstrap);  // Should be 'object'

// Check if modal instance exists
const modalElement = document.getElementById('myModal');
const modal = bootstrap.Modal.getInstance(modalElement);
console.log(modal);
```

**Solutions:**

1. **Ensure JavaScript is Loaded:**
   ```html
   <!-- Must include Bootstrap JS -->
   <script src="bootstrap.bundle.min.js"></script>
   ```

2. **Check Modal Structure:**
   ```html
   <!-- Modal must have proper structure -->
   <div class="modal fade" id="myModal" tabindex="-1">
     <div class="modal-dialog">
       <div class="modal-content">
         <!-- Content -->
       </div>
     </div>
   </div>
   ```

3. **Check for JavaScript Errors:**
   - Open browser console (F12)
   - Look for error messages
   - Fix any conflicting scripts

#### Issue: Dropdown Not Positioning Correctly

**Symptoms:** Dropdown appears in wrong position or gets cut off.

**Solutions:**

1. **Ensure Popper.js is Included:**
   ```html
   <!-- Use bootstrap.bundle.min.js (includes Popper) -->
   <script src="bootstrap.bundle.min.js"></script>
   ```

2. **Check Container Overflow:**
   ```css
   /* Parent containers shouldn't have overflow: hidden */
   .parent {
     overflow: visible !important;
   }
   ```

3. **Set Proper Boundary:**
   ```javascript
   const dropdown = new bootstrap.Dropdown(element, {
     boundary: 'viewport'
   });
   ```

#### Issue: Carousel Not Auto-playing

**Symptoms:** Carousel doesn't cycle through slides automatically.

**Solutions:**

1. **Add data-bs-ride Attribute:**
   ```html
   <div class="carousel slide" data-bs-ride="carousel">
   ```

2. **Initialize with JavaScript:**
   ```javascript
   const carousel = new bootstrap.Carousel('#myCarousel', {
     interval: 5000,
     ride: 'carousel'
   });
   ```

3. **Check for Pause on Hover:**
   ```javascript
   // Disable pause on hover
   const carousel = new bootstrap.Carousel('#myCarousel', {
     pause: false
   });
   ```

### Styling Issues

#### Issue: Grid Columns Not Aligning

**Symptoms:** Columns stack unexpectedly or don't fill width.

**Solutions:**

1. **Check Row Structure:**
   ```html
   <div class="container">
     <div class="row">
       <div class="col">Content</div>
     </div>
   </div>
   ```

2. **Verify Column Classes:**
   ```html
   <!-- Columns must sum to 12 or use col-auto -->
   <div class="row">
     <div class="col-6">Half</div>
     <div class="col-6">Half</div>
   </div>
   ```

3. **Check for Custom CSS:**
   ```css
   /* Remove conflicting styles */
   .row {
     display: flex; /* Should be set by Bootstrap */
   }
   ```

#### Issue: RTL (Right-to-Left) Not Working

**Symptoms:** RTL layout not applying correctly.

**Solutions:**

1. **Use RTL CSS File:**
   ```html
   <link href="bootstrap.rtl.min.css" rel="stylesheet">
   ```

2. **Set HTML Direction:**
   ```html
   <html dir="rtl" lang="ar">
   ```

3. **Rebuild with RTL:**
   ```bash
   npm run css-rtl
   ```

---

## Maintenance Procedures

### Regular Maintenance Tasks

#### Weekly Tasks

1. **Monitor GitHub Issues:**
   - Triage new issues
   - Respond to bug reports
   - Label appropriately

2. **Review Pull Requests:**
   - Code review
   - Test changes
   - Merge or request changes

3. **Update Dependencies:**
   ```bash
   npm outdated
   npm update
   ```

#### Monthly Tasks

1. **Security Audit:**
   ```bash
   npm audit
   npm audit fix
   ```

2. **Performance Review:**
   ```bash
   npm run bundlewatch
   ```

3. **Browser Testing:**
   ```bash
   npm run js-test-cloud
   ```

#### Quarterly Tasks

1. **Major Dependency Updates:**
   ```bash
   npm run update-deps
   ```

2. **Documentation Review:**
   - Update examples
   - Fix broken links
   - Add new features

3. **Accessibility Audit:**
   - Run aXe DevTools
   - Test with screen readers
   - Verify keyboard navigation

### Version Maintenance

#### Semantic Versioning

Bootstrap follows semantic versioning (MAJOR.MINOR.PATCH):

- **MAJOR**: Breaking changes
- **MINOR**: New features, backward compatible
- **PATCH**: Bug fixes, backward compatible

#### Updating Version Number

```bash
# Use the version update script
node build/change-version.mjs 5.3.9
```

This updates:
- `package.json`
- `package-lock.json`
- `scss/_functions.scss`
- `js/src/base-component.js`

#### Maintaining Multiple Versions

**Active Branches:**
- `main`: Development for next major version
- `v5-dev`: Current stable (5.3.x)
- `v4-dev`: Legacy support (4.6.x)

**Branch Strategy:**
```bash
# Bug fixes go to stable branch
git checkout v5-dev
# Make fixes
git push origin v5-dev

# Features go to main
git checkout main
# Add features
git push origin main
```

---

## Backup and Recovery Processes

### Source Code Backup

**Primary Repository:** GitHub  
**Backup Locations:**
- GitHub's own backup systems
- Developer local clones
- Mirror repositories (if configured)

**Recovery Process:**
```bash
# Clone from GitHub
git clone https://github.com/twbs/bootstrap.git

# Or restore from backup
git clone <backup-url>
```

### npm Package Recovery

If a published npm version is accidentally unpublished:

```bash
# Republish from git tag
git checkout v5.3.8
npm install
npm run dist
npm publish
```

### Documentation Recovery

Documentation is built from source and deployed to:
- **Primary**: Netlify (getbootstrap.com)
- **Source**: Git repository (`site/` directory)

**Recovery:**
```bash
# Rebuild documentation
npm install
npm run docs-build

# Redeploy (handled by Netlify on push to main)
git push origin main
```

---

## Performance Tuning Guidelines

### Optimizing Build Performance

#### Parallel Builds

Use `npm-run-all` for parallel execution:

```bash
# Run CSS and JS builds in parallel
npm-run-all --parallel css js
```

#### Incremental Builds

Use watch mode during development:

```bash
# Watch and rebuild on change
npm run watch
```

#### Caching

Enable caching for faster builds:

```bash
# ESLint uses cache
npm run js-lint  # Creates .cache/.eslintcache

# Stylelint uses cache
npm run css-lint  # Creates .cache/.stylelintcache
```

### Optimizing Bundle Size

#### Import Only What You Need

**JavaScript:**
```javascript
// Instead of importing everything
import 'bootstrap';

// Import specific components
import { Modal, Dropdown, Tooltip } from 'bootstrap';
```

**Sass:**
```scss
// Instead of importing everything
@import "bootstrap/scss/bootstrap";

// Import specific components
@import "bootstrap/scss/functions";
@import "bootstrap/scss/variables";
@import "bootstrap/scss/mixins";
@import "bootstrap/scss/grid";
@import "bootstrap/scss/buttons";
```

#### Tree Shaking

Modern bundlers automatically remove unused code:

**Webpack:**
```javascript
// webpack.config.js
module.exports = {
  mode: 'production',
  optimization: {
    usedExports: true,
    sideEffects: false
  }
};
```

**Vite:**
Tree shaking is enabled by default in production mode.

#### Minification

Always use minified files in production:

```html
<!-- Development -->
<link href="bootstrap.css" rel="stylesheet">
<script src="bootstrap.bundle.js"></script>

<!-- Production -->
<link href="bootstrap.min.css" rel="stylesheet">
<script src="bootstrap.bundle.min.js"></script>
```

### Runtime Performance

#### Reduce DOM Manipulation

```javascript
// Bad: Multiple DOM updates
document.getElementById('modal1').classList.add('show');
document.getElementById('modal2').classList.add('show');
document.getElementById('modal3').classList.add('show');

// Good: Batch updates
requestAnimationFrame(() => {
  const modals = document.querySelectorAll('.modal');
  modals.forEach(modal => modal.classList.add('show'));
});
```

#### Lazy Load Components

```javascript
// Only initialize when needed
const myModal = document.getElementById('myModal');
myModal.addEventListener('show.bs.modal', function (event) {
  // Initialize modal content here
}, { once: true });
```

#### Debounce Window Events

```javascript
let resizeTimer;
window.addEventListener('resize', function() {
  clearTimeout(resizeTimer);
  resizeTimer = setTimeout(function() {
    // Handle resize
  }, 250);
});
```

---

## Security Considerations

### Content Security Policy (CSP)

Bootstrap is CSP-compatible. Recommended CSP headers:

```
Content-Security-Policy: 
  default-src 'self'; 
  style-src 'self' 'unsafe-inline' cdn.jsdelivr.net; 
  script-src 'self' cdn.jsdelivr.net; 
  img-src 'self' data:;
```

### Subresource Integrity (SRI)

Always use SRI when loading from CDN:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" 
      rel="stylesheet" 
      integrity="sha384-..." 
      crossorigin="anonymous">
```

### XSS Prevention

Bootstrap includes HTML sanitization for:
- Tooltips
- Popovers
- Modals (when using templates)

```javascript
// Safe: Uses sanitizer
const tooltip = new bootstrap.Tooltip(element, {
  html: true,
  title: '<strong>Title</strong>'  // Automatically sanitized
});

// Configure sanitizer
const myDefaultAllowList = bootstrap.Tooltip.Default.allowList;
myDefaultAllowList.table = [];
myDefaultAllowList.td = [];
myDefaultAllowList.th = [];
```

### Dependency Security

Keep dependencies updated:

```bash
# Check for vulnerabilities
npm audit

# Fix automatically
npm audit fix

# Check outdated packages
npm outdated
```

---

## CI/CD Integration

### GitHub Actions Workflows

Bootstrap uses GitHub Actions for continuous integration:

#### JavaScript Tests (`.github/workflows/js.yml`)
```yaml
name: JS Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm install
      - run: npm run js-lint
      - run: npm run js-test
```

#### CSS Tests (`.github/workflows/css.yml`)
```yaml
name: CSS Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm install
      - run: npm run css-lint
      - run: npm run css-test
```

#### Documentation Build (`.github/workflows/docs.yml`)
```yaml
name: Docs
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm install
      - run: npm run docs-build
```

### Netlify Deployment

Documentation auto-deploys via Netlify:

**netlify.toml:**
```toml
[build]
  command = "npm run netlify"
  publish = "_site"

[build.environment]
  NODE_VERSION = "18"
```

---

*This operational guide provides comprehensive information for deploying, maintaining, and troubleshooting Bootstrap in production environments.*
