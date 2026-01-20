# AGENTS.md

This file provides guidelines for agentic coding agents working in this repository.

## Project Overview

This is a simple, static photo gallery website. It uses plain HTML, CSS, and JavaScript, with no build tools or frameworks. The goal is to keep the codebase clean, simple, and maintainable.

## Build, Lint, and Test Commands

There is no formal build process for this project. However, here are some recommended commands for local development, linting, and formatting.

### Local Development

To serve the website locally and see changes live, you can use a simple HTTP server. If you have Node.js installed, you can use the `live-server` package:

```bash
# Install live-server globally (if you haven't already)
npm install -g live-server

# Serve the website
live-server
```

### Formatting and Linting

To maintain consistent code style, we recommend using Prettier for formatting and ESLint for identifying potential issues in JavaScript.

First, you would need to set up a `package.json` and install these dependencies:

```bash
npm init -y
npm install --save-dev prettier eslint
```

**Formatting (Prettier)**

Create a `.prettierrc` file with your desired configuration, for example:

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2
}
```

Then, you can format the code using the following command:

```bash
# Format all HTML, CSS, and JavaScript files
prettier --write "**/*.{html,css,js}"
```

**Linting (ESLint)**

Set up an ESLint configuration file (`.eslintrc.json`):

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  }
}
```

Then, lint the JavaScript files:

```bash
eslint "**/*.js"
```

### Testing

There are currently no automated tests for this project. Given its simplicity, manual testing is sufficient. When making changes, please test the following:

-   The gallery layout is responsive and displays correctly on different screen sizes.
-   Clicking on a thumbnail opens the lightbox.
-   The close button and clicking outside the image in the lightbox closes it.

## Code Style Guidelines

### General

-   **File Naming**: Use lowercase and kebab-case for file names (e.g., `contact-form.html`).
-   **Indentation**: Use 2 spaces for indentation.
-   **Comments**: Use comments to explain the *why*, not the *what*. Keep comments concise and up-to-date.

### HTML

-   **Semantics**: Use semantic HTML5 elements (`<header>`, `<main>`, `<footer>`, etc.) to structure the page.
-   **Accessibility**: Ensure all images have a descriptive `alt` attribute.
-   **Clarity**: Write clean and readable HTML. Avoid unnecessary `div`s.

### CSS

-   **Naming Convention**: The project uses a BEM-like naming convention for classes (e.g., `.gallery-item`, `.lightbox-content`). Please follow this convention.
-   **Organization**: Group related CSS rules together. Start with global styles, then layout, then components.
-   **Units**: Use `rem` for font sizes and `px` for borders. Use `rem` or `%` for layout dimensions where appropriate.

### JavaScript

-   **Modern JavaScript**: Use modern ES6+ features like `const`, `let`, arrow functions, and template literals.
-   **Strict Mode**: While not explicitly used, writing code that is compliant with strict mode is encouraged.
-   **DOM Manipulation**: Keep DOM manipulation clean and efficient. Cache DOM elements in variables if they are accessed multiple times.
-   **Error Handling**: Although the current JavaScript is simple, for any new functionality, add basic error handling where appropriate (e.g., checking if an element exists before trying to add an event listener to it).
-   **No jQuery**: This project uses plain JavaScript. Do not introduce jQuery or other large libraries.
