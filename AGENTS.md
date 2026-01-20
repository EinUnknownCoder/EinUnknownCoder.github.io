# AGENTS.md

This file provides comprehensive guidelines for agentic coding agents (AI) operating within this repository.
It defines the buildless environment, manual testing protocols, and strict code style conventions to ensure consistency.

## 1. Environment & Architecture

**Project Type**: Static Website (Photo Gallery).
**Stack**: HTML5, CSS3, Vanilla JavaScript (ES6+).
**Dependencies**: Zero-dependency architecture (no npm/bundlers). External assets (Fonts/Icons) via CDN are permitted.

### Key Constraints
-   **No Build Tools**: Do not introduce Webpack, Parcel, Vite, or similar bundlers.
-   **No Frameworks**: Do not introduce React, Vue, jQuery, or Bootstrap.
-   **Direct Execution**: The project is designed to run directly in a browser or via a simple static file server.

## 2. Operational Commands

Since there is no `package.json`, standard `npm` scripts are unavailable. Use `npx` for tooling or perform tasks manually.

### Serving the Application
To preview changes, serve the root directory using a static server.
```bash
# Recommended: Use live-server via npx
npx live-server --port=8080 --entry-file=index.html
```

### Formatting & Linting
Maintain code quality using standard tools via `npx`.
```bash
# Format Code (Prettier)
npx prettier --write "**/*.{html,css,js}" --tab-width 4 --single-quote

# Lint JavaScript (ESLint)
# Note: Requires a config file. If none exists, rely on manual review or standard rules.
npx eslint "js/**/*.js"
```

### Testing Strategy
**Status**: No automated testing framework exists.
**Requirement**: You must perform **Manual Verification** for every change.

#### Manual Test Protocol (Required)
Perform these checks before marking a task as complete:
1.  **Console Check**:
    -   Open Developer Tools (F12).
    -   Reload the page.
    -   Verify **zero** console errors or warnings.
2.  **Layout Responsiveness**:
    -   View at **Desktop** (>1024px): Grid should show multiple columns.
    -   View at **Mobile** (<480px): Grid should collapse to 1 or 2 columns.
3.  **Core Functionality (Lightbox)**:
    -   **Open**: Click any `.gallery-item` image. Verify `#lightbox` appears with the correct high-res image.
    -   **Close (Button)**: Click the `×` button. Verify `#lightbox` disappears.
    -   **Close (Background)**: Click the dark background (overlay). Verify `#lightbox` disappears.
    -   **Navigation**: (If implemented) Verify next/prev buttons work without errors.

## 3. Code Style Guidelines

Adhere strictly to these conventions to match existing code.

### JavaScript (`js/main.js`)
-   **Indentation**: **4 spaces**.
-   **Quotes**: Single quotes `'` preferred.
-   **Semicolons**: **Yes**, use semicolons at the end of statements.
-   **Variables**: Use `const` for immutables, `let` for mutables. Avoid `var`.
-   **Functions**: Use Arrow functions `() => {}` for callbacks.
-   **DOM Access**:
    -   Cache elements at the top of `DOMContentLoaded`.
    -   Use `document.querySelector` / `querySelectorAll` for complex selectors.
    -   Use `document.getElementById` for ID selectors.
-   **Event Listeners**:
    -   Wrap all logic in `document.addEventListener('DOMContentLoaded', ...)` to ensure DOM readiness.
    -   Clean up listeners if elements are removed (though rare in this static app).

### CSS (`css/style.css`)
-   **Indentation**: **4 spaces**.
-   **Selectors**:
    -   Use BEM-like naming for components (e.g., `.gallery`, `.gallery-item`).
    -   Use IDs (`#lightbox`) sparingly, mainly for unique global states or overlays.
-   **Units**:
    -   `rem`: Padding, margins, font-sizes.
    -   `px`: Borders, minimal widths.
    -   `%`: Layout widths where Grid/Flex isn't used.
-   **Layout**: Prefer CSS Grid and Flexbox over floats.

### HTML (`index.html`)
-   **Indentation**: **4 spaces**.
-   **Semantics**: Use `<header>`, `<main>`, `<footer>`, `<section>`.
-   **Accessibility (A11y)**:
    -   **Images**: Must have descriptive `alt` attributes.
    -   **Interactive Elements**: Buttons/Links must have focus states and aria-labels if icon-only.
-   **Lazy Loading**: Use `data-src` for high-resolution images intended for the lightbox, keeping initial load light.

## 4. Development Workflow for Agents

1.  **Analysis**:
    -   Read `index.html`, `css/style.css`, and `js/main.js` to establish context.
    -   Identify if the change requires modifying structure (HTML), style (CSS), or logic (JS).
2.  **Implementation**:
    -   Make atomic changes.
    -   Ensure new CSS classes follow the existing naming convention.
    -   Ensure new JS functions document their purpose if complex.
3.  **Verification**:
    -   Run the **Manual Test Protocol**.
    -   If a bug is found, fix it *before* reporting completion.
    -   Do not break existing functionality (Regression Testing).

## 5. Tooling Rules

-   **Copilot / AI Assistants**:
    -   Context Awareness: Always read the referenced CSS file when generating JS that manipulates classes.
    -   Simplicity: Reject suggestions that import libraries (e.g., `import { modal } from 'bootstrap'`). Rewrite logic in vanilla JS.
-   **Cursor Rules**:
    -   If `.cursor/rules` exists, those rules take precedence.
    -   Otherwise, default to: "Write clean, readable, zero-dependency code."

## 6. Directory Structure

```text
/
├── css/
│   └── style.css       # Global styles
├── js/
│   └── main.js         # Main application logic
├── images/             # Static assets
├── index.html          # Entry point
├── AGENTS.md           # This file
└── README.md           # General project info
```

When creating new files, place them in the appropriate subdirectory. Do not clutter the root.

## 7. Error Handling & Edge Cases

-   **Missing Elements**:
    -   Example: `const btn = document.querySelector('.btn'); if (btn) { ... }`
    -   Always check if an element exists before attaching listeners to avoid runtime errors on pages where the element is absent.
-   **Network Errors**:
    -   For image loading, consider adding `onerror` handlers to show placeholders if an image fails to load.

## 8. Commit & Version Control

-   **Messages**: Use conventional commits (e.g., `feat: add swipe support`, `fix: lightbox close issue`).
-   **Scope**: Keep commits small and focused on a single logical change.
