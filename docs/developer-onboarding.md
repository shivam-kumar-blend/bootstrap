# Bootstrap Developer Onboarding Guide

Welcome to the Bootstrap development team! This guide will help you get set up and started with contributing to Bootstrap.

## Prerequisites and Required Tools

### Required Software

Before you begin, ensure you have the following installed:

#### 1. Node.js and npm
- **Version Required**: Node.js 18.x or higher
- **Download**: [nodejs.org](https://nodejs.org/)
- **Verify Installation**:
  ```bash
  node --version  # Should be v18.x or higher
  npm --version   # Should be 9.x or higher
  ```

#### 2. Git
- **Version Required**: Git 2.x or higher
- **Download**: [git-scm.com](https://git-scm.com/)
- **Verify Installation**:
  ```bash
  git --version
  ```

#### 3. Code Editor
We recommend:
- **Visual Studio Code** (with extensions: ESLint, Stylelint, EditorConfig)
- **WebStorm** or **Sublime Text** are also popular choices

### Optional but Recommended

- **GitHub CLI**: For easier GitHub integration
- **BrowserStack Account**: For cross-browser testing (provided by the team)
- **Astro Knowledge**: For documentation website work

## Step-by-Step Setup Instructions

### 1. Clone the Repository

```bash
# Clone the repository
git clone https://github.com/twbs/bootstrap.git

# Navigate to the directory
cd bootstrap
```

### 2. Install Dependencies

```bash
# Install all npm dependencies
npm install
```

This will install:
- Build tools (Rollup, Sass, PostCSS, Terser)
- Testing frameworks (Karma, Jasmine)
- Linting tools (ESLint, Stylelint)
- Documentation tools (Astro)
- Other development dependencies

**Expected Time**: 2-5 minutes depending on internet speed

### 3. Build Bootstrap

```bash
# Build both CSS and JavaScript
npm run dist
```

This command:
- Compiles Sass to CSS
- Adds vendor prefixes with autoprefixer
- Generates RTL (right-to-left) CSS variants
- Minifies CSS files
- Compiles JavaScript with Rollup
- Minifies JavaScript files

**Expected Output**: Compiled files in `/dist` directory

### 4. Run the Development Server

```bash
# Start development server with watch mode
npm start
```

This will:
- Watch for file changes in `scss/` and `js/` directories
- Automatically recompile on changes
- Start documentation server on http://localhost:9001

**Access the docs**: Open your browser to http://localhost:9001

### 5. Verify Setup

Run the test suite to ensure everything works:

```bash
# Run all tests
npm test
```

This executes:
- JavaScript linting
- CSS linting
- JavaScript unit tests
- CSS tests
- Documentation build
- Documentation validation

**Expected Result**: All tests should pass ✓

## Project Structure Overview

### Key Directories

```
bootstrap/
├── dist/                    # Compiled/built files (generated, not in git)
│   ├── css/                # Compiled CSS files
│   └── js/                 # Compiled JavaScript files
│
├── js/                     # JavaScript source
│   ├── src/                # Component source files
│   │   ├── alert.js        # Alert component
│   │   ├── modal.js        # Modal component
│   │   ├── dropdown.js     # Dropdown component
│   │   └── ...             # Other components
│   ├── dist/               # Individual component builds
│   └── tests/              # JavaScript tests
│
├── scss/                   # Sass source files
│   ├── _variables.scss     # Sass variables (colors, spacing, etc.)
│   ├── _mixins.scss        # Sass mixins
│   ├── _buttons.scss       # Button styles
│   ├── _forms.scss         # Form styles
│   ├── bootstrap.scss      # Main entry point
│   ├── forms/              # Form-related partials
│   ├── helpers/            # Helper utilities
│   ├── mixins/             # Individual mixin files
│   └── utilities/          # Utility classes
│
├── site/                   # Documentation website
│   ├── src/                # Astro source files
│   └── dist/               # Built documentation (generated)
│
├── build/                  # Build scripts
│   ├── rollup.config.mjs   # Rollup configuration
│   ├── postcss.config.mjs  # PostCSS configuration
│   └── ...                 # Other build utilities
│
└── .github/                # GitHub-specific files
    ├── workflows/          # CI/CD workflows
    └── CONTRIBUTING.md     # Contribution guidelines
```

### Important Files

- **package.json**: npm scripts and dependencies
- **.eslintrc.json**: JavaScript linting rules
- **.stylelintrc.json**: CSS/Sass linting rules
- **.editorconfig**: Editor configuration
- **.babelrc.js**: Babel configuration for JavaScript transpilation

## First Task Walkthrough

Let's walk through a simple task: Adding a utility class to Bootstrap.

### Task: Add a New Text Decoration Utility

#### Step 1: Locate the Utilities File

```bash
# Open the utilities API file
code scss/utilities/_api.scss
```

#### Step 2: Understand the Structure

Utilities are defined in the `$utilities` map. Each utility has:
- `property`: CSS property to set
- `class`: Class name prefix
- `values`: Possible values

#### Step 3: Add Your Utility

Find the text-decoration section and verify it exists:

```scss
"text-decoration": (
  property: text-decoration,
  values: none underline line-through
),
```

If you wanted to add `overline`:

```scss
"text-decoration": (
  property: text-decoration,
  values: none underline line-through overline
),
```

#### Step 4: Build and Test

```bash
# Compile CSS
npm run css-compile

# Check the compiled CSS
cat dist/css/bootstrap.css | grep "text-decoration"
```

You should see `.text-decoration-overline` generated.

#### Step 5: Test in Documentation

Add an example in the docs:

```bash
# Edit the utilities documentation
code site/src/content/docs/5.3/utilities/text.mdx
```

Add your example:

```html
<p class="text-decoration-overline">This text has an overline.</p>
```

#### Step 6: Preview Your Changes

```bash
# Start the dev server if not running
npm start

# Visit http://localhost:9001/docs/5.3/utilities/text/
```

#### Step 7: Lint Your Code

```bash
# Run linting
npm run lint

# Fix auto-fixable issues
npm run css-lint-stylelint -- --fix
```

#### Step 8: Run Tests

```bash
# Run CSS tests
npm run css-test

# Run full test suite
npm test
```

#### Step 9: Commit Your Changes

```bash
# Stage your changes
git add scss/utilities/_api.scss
git add site/src/content/docs/5.3/utilities/text.mdx

# Commit with a descriptive message
git commit -m "Add overline value to text-decoration utility"
```

## Common Development Workflows

### Working on CSS/Sass

```bash
# Watch Sass files and recompile on changes
npm run watch-css-main

# Compile CSS only
npm run css

# Run CSS linter
npm run css-lint

# Run CSS tests
npm run css-test
```

### Working on JavaScript

```bash
# Watch JavaScript files and recompile on changes
npm run watch-js-main

# Compile JavaScript only
npm run js

# Run JavaScript linter
npm run js-lint

# Run JavaScript tests
npm run js-test

# Run tests in debug mode
npm run js-debug
```

### Working on Documentation

```bash
# Start documentation server
npm run docs-serve

# Build documentation
npm run docs-build

# Format documentation with Prettier
npm run docs-prettier-format

# Validate HTML in documentation
npm run docs-vnu
```

### Running Specific Tests

```bash
# Run only Karma tests
npm run js-test-karma

# Run tests with jQuery
npm run js-test-jquery

# Run on BrowserStack (requires credentials)
npm run js-test-cloud

# Run integration tests
npm run js-test-integration-bundle
```

## Development Best Practices

### Code Style

1. **JavaScript**
   - Use ES6+ features
   - Follow existing code style (enforced by ESLint)
   - Add JSDoc comments for public methods
   - Keep components modular and focused

2. **Sass/CSS**
   - Follow BEM-like naming conventions
   - Use variables for all values
   - Maintain mobile-first approach
   - Add comments for complex logic

3. **HTML**
   - Use semantic HTML5 elements
   - Include ARIA attributes where needed
   - Ensure keyboard accessibility
   - Test with screen readers

### Testing Guidelines

1. **Write Tests First** (TDD approach when possible)
2. **Test Edge Cases**: Empty states, long content, etc.
3. **Cross-browser Testing**: Use BrowserStack for older browsers
4. **Accessibility Testing**: Use aXe or similar tools
5. **Visual Regression**: Compare before/after screenshots

### Git Workflow

1. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Small, Focused Commits**
   ```bash
   git commit -m "Brief description of change"
   ```

3. **Keep Your Branch Updated**
   ```bash
   git fetch origin
   git rebase origin/main
   ```

4. **Push Your Branch**
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Open a Pull Request** on GitHub

### Code Review Process

- All code must be reviewed before merging
- Address all review comments
- Ensure CI/CD checks pass
- Get approval from at least one maintainer
- Squash commits when merging

## Resources and Learning Materials

### Official Resources

1. **Bootstrap Documentation**: https://getbootstrap.com/docs/5.3/
2. **GitHub Repository**: https://github.com/twbs/bootstrap
3. **Contributing Guide**: https://github.com/twbs/bootstrap/blob/main/.github/CONTRIBUTING.md

### Sass Resources

- **Sass Documentation**: https://sass-lang.com/documentation
- **Sass Guidelines**: https://sass-guidelin.es/

### JavaScript Resources

- **MDN Web Docs**: https://developer.mozilla.org/
- **ES6 Features**: https://github.com/lukehoban/es6features
- **Popper.js**: https://popper.js.org/ (used for positioning)

### Accessibility Resources

- **ARIA Authoring Practices**: https://www.w3.org/WAI/ARIA/apg/
- **WebAIM**: https://webaim.org/
- **A11y Project**: https://www.a11yproject.com/

### Build Tool Resources

- **Rollup**: https://rollupjs.org/
- **PostCSS**: https://postcss.org/
- **Astro**: https://docs.astro.build/

## Team Contacts and Communication Channels

### Communication Channels

- **GitHub Discussions**: For questions and long-form discussions
- **GitHub Issues**: For bug reports and feature requests
- **Discord**: Real-time chat with the community
- **Twitter**: @getbootstrap for announcements

### Key Maintainers

- See [GitHub Contributors](https://github.com/twbs/bootstrap/graphs/contributors)
- Core team listed in package.json and CODEOWNERS

### Getting Help

1. **Search Existing Issues**: Someone may have had the same problem
2. **Check Documentation**: Comprehensive guides available
3. **Ask in Discussions**: Community is helpful and responsive
4. **Stack Overflow**: Tag questions with `bootstrap-5`

## Development Environment Tips

### VS Code Extensions

Install these extensions for the best experience:

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "stylelint.vscode-stylelint",
    "editorconfig.editorconfig",
    "astro-build.astro-vscode"
  ]
}
```

### Useful Aliases

Add these to your `.bashrc` or `.zshrc`:

```bash
# Bootstrap shortcuts
alias bs-build="npm run dist"
alias bs-watch="npm start"
alias bs-test="npm test"
alias bs-lint="npm run lint"
```

### Browser DevTools

- **Chrome DevTools**: Best for debugging JavaScript
- **Firefox Developer Edition**: Great for CSS Grid debugging
- **Safari Web Inspector**: For iOS-specific issues

## Troubleshooting Common Issues

### Issue: npm install fails

**Solution**: 
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and package-lock.json
rm -rf node_modules package-lock.json

# Reinstall
npm install
```

### Issue: Sass compilation errors

**Solution**:
```bash
# Ensure you're using the correct Sass version
npm list sass

# Should match version in package.json (1.78.0)
```

### Issue: Tests fail locally but pass on CI

**Solution**:
```bash
# Ensure your branch is up to date
git fetch origin
git rebase origin/main

# Clear any cached test results
rm -rf .cache
npm test
```

### Issue: Documentation not updating

**Solution**:
```bash
# Stop the server (Ctrl+C)
# Clear Astro cache
rm -rf site/.astro

# Restart
npm run docs-serve
```

## Next Steps

Now that you're set up:

1. **Explore the Codebase**: Read through component files to understand patterns
2. **Pick an Issue**: Look for "good first issue" labels on GitHub
3. **Join the Community**: Introduce yourself on Discord
4. **Read the Docs**: Familiarize yourself with all components
5. **Start Contributing**: Small improvements are always welcome!

Welcome aboard, and happy coding! 🚀

---

*If you have any questions or need clarification, don't hesitate to ask in GitHub Discussions or Discord.*
