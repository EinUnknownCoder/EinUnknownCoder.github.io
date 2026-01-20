# AGENTS.md

This file defines the strict protocols, code style, and operational workflow for AI agents and developers working in this repository.
The project is a buildless, static website (HTML/CSS/JS) requiring manual verification and strict adherence to conventions.

## 1. Environment & Architecture

-   **Type**: Static Website (Photo Gallery).
-   **Stack**: HTML5, CSS3, Vanilla JavaScript (ES6+).
-   **Language**: German (`lang="de"`). User-facing text must be in German.
-   **Dependencies**: ZERO. No `npm`, `node_modules`, or bundlers.
-   **Asset Strategy**:
    -   Local images in `/images`.
    -   Fonts/Icons via standard CDNs (Google Fonts) are allowed.
    -   No external JS libraries (jQuery, Bootstrap, etc.) unless explicitly requested.

### System Constraints
-   **No Node.js/NPM**: The environment may not have `node` or `npm`. Do not rely on `npx` commands.
-   **No Build Step**: Code must run directly in the browser. Use native ES modules if needed, but currently `main.js` is a standard script.

## 2. Operational Commands

### Serving the Application
Since `npm` is unavailable, use Python to serve the static files for verification.

```bash
# Start a local server on port 8080
python3 -m http.server 8080 &
```

### Formatting & Linting
**Automated formatters are not available.** You must manually adhere to the code style.
-   **Do not** reformat entire files. Only format the lines you change.
-   **Do not** change indentation style (spaces vs tabs) of existing files.

### Testing Strategy (Manual Only)
There are no automated tests. You must manually verify changes using the **Single Test Protocol**.

#### The "Single Test" Protocol
For every change, perform these 3 specific checks:

1.  **Console Health**:
    -   Open DevTools. Reload. Ensure **0 console errors**.
2.  **Visual Layout**:
    -   **Desktop**: Grid layout (3+ columns).
    -   **Mobile**: Single column layout.
    -   Verify no horizontal scrollbars appear unintentionally.
3.  **Feature Logic**:
    -   **Lightbox**: Click an image. Verify it opens. Click 'X'. Verify it closes.
    -   **Images**: Ensure all placeholders load.
    -   **Responsiveness**: Resize window to ensure elements flow correctly.

## 3. Code Style Guidelines

You must match the existing codebase exactly.

### JavaScript (`js/main.js`)
-   **Indentation**: 4 spaces.
-   **Quotes**: Single quotes (`'`) preferred.
-   **Semicolons**: **ALWAYS** use semicolons.
-   **Variables**: `const` by default, `let` if reassignment is needed. No `var`.
-   **DOM**:
    -   Cache selectors at the top of the scope/function.
    -   Use `document.getElementById` for IDs, `querySelector` for classes.
    -   Always wrap execution in `DOMContentLoaded`.
-   **Functions**: Arrow functions `() => {}` for callbacks/anonymous functions.

### CSS (`css/style.css`)
-   **Indentation**: 4 spaces.
-   **Syntax**: Standard CSS (no SCSS/Sass).
-   **Naming**: BEM-ish (e.g., `.gallery`, `.gallery-item`).
-   **Units**: `rem` for spacing/font-size, `%`/`fr` for layout, `px` for borders.
-   **Variables**: Use `:root` variables for colors and spacing.

### HTML (`index.html`)
-   **Indentation**: 4 spaces.
-   **Structure**: Semantic tags (`<header>`, `<main>`, `<footer>`, `<section>`).
-   **Accessibility**:
    -   All `<img>` tags MUST have a descriptive `alt`.
    -   Interactive elements need `aria-label` if text is not visible.

## 4. Agent Workflow

1.  **Analyze**:
    -   Read `AGENTS.md` (this file).
    -   Read `index.html` and relevant JS/CSS files to build a mental model.
    -   Check for existing patterns (e.g., how the Lightbox is toggled) before writing new code.

2.  **Plan**:
    -   Determine if the request requires Structure (HTML), Style (CSS), or Logic (JS).
    -   Propose a plan that uses *only* vanilla technologies.

3.  **Implement**:
    -   Write code using `edit` or `write`.
    -   **CRITICAL**: Use absolute paths (e.g., `/home/user/repo/css/style.css`).
    -   **CRITICAL**: Maintain 4-space indentation.

4.  **Verify**:
    -   Start the python server if not running.
    -   Review your changes. If you added a class, did you add the CSS?
    -   If you added an ID, is it unique?

## 5. Directory Structure

```text
/
├── css/
│   └── style.css       # Global styles
├── js/
│   └── main.js         # Application logic
├── images/             # Local image assets
├── index.html          # Main entry point
└── AGENTS.md           # This file
```

## 6. Error Handling & Edge Cases

-   **Defensive DOM**:
    -   Always check if an element exists before adding listeners.
    -   `const btn = document.getElementById('btn'); if(btn) { ... }`
-   **Image Loading**:
    -   Assume images might fail. The CSS should handle layout gracefully if an image is missing (e.g., background colors).

## 7. Version Control

-   **Commit Messages**: Conventional Commits (e.g., `feat: add footer links`, `fix: mobile padding`).
-   **Scope**: Atomic commits. One feature/fix per commit.
-   **No Reverts**: Unless critical. Fix forward.

## 8. Specific Rules (Copilot/Cursor)

-   **Cursor**: No specific `.cursorrules` exist, so follow this file implicitly.
-   **Copilot**: No `.github/copilot-instructions.md` exist.
-   **General AI Rule**: Do not suggest "modern" build stacks (React/Vite) for this project. Keep it simple and native.

---
*Last Updated: 2026-01-20*
