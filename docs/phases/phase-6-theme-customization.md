# Phase 6: Theme customization guide for Roads Light

Overview
- This phase documents how to customize the Roads Light theme used by the map UI, including tokens, runtime switching, extending the theme with brand colors, and integrating custom brand styles.

Tokens (CSS custom properties)
- Road styling tokens (used by map/controls):
  - --roads-road-color
  - --roads-road-outline-color
  - --roads-background-color
  - --roads-background-elevated
  - --roads-label-color
  - --roads-surface-color
  - --roads-border-color
  - --roads-shadow-color
- UI and typography tokens (brand-safe defaults):
  - --color-text
  - --font-family-sans
  - --font-size-base
- Brand tokens (recommended to override project-wide):
  - --brand-color
  - --brand-contrast-color
  - --brand-font

Where they live
- Tokens are declared in the global CSS (or a shared CSS module) and are consumed by components via var(--token-name).
- The Roads Light theme uses a data-theme attribute on the root element to switch between themes.

Theme switching at runtime
- Approach: toggle a data-theme attribute on the root element (e.g., document.documentElement).
- Example (vanilla JS):
  ```js
  export type Theme = 'roads-light' | 'roads-dark';
  export const applyTheme = (theme: Theme) => {
    document.documentElement.setAttribute('data-theme', theme);
    localStorage.setItem('theme', theme);
  };
  // On app startup, read saved theme:
  const saved = localStorage.getItem('theme') ?? 'roads-light';
  applyTheme(saved as Theme);
  ```
- CSS selectors for runtime switching:
  ```css
  /* Road colors for light theme */
  [data-theme="roads-light"] {
    --roads-road-color: #e5e7eb;
    --roads-background-color: #ffffff;
    --color-text: #1f2937;
  }
  [data-theme="roads-dark"] {
    --roads-road-color: #2b2b2b;
    --roads-background-color: #0f111a;
    --color-text: #e5e7eb;
  }
  ```
- If you already have a CSS-in-JS or SCSS layer, you can also update tokens in that layer using the same CSS variable names.

Extending the theme with custom colors
- To add new colors, declare new CSS tokens and then use them in components.
- Example:
  ```css
  :root {
    --roads-accent-color: #10b981; /* mint */
  }
  [data-theme="roads-light"] {
    --roads-accent-color: #10b981;
  }
  [data-theme="roads-dark"] {
    --roads-accent-color: #34d399;
  }
  ```
- Use token fallbacks so existing themes remain functional if a token is missing:
  ```css
  .button {
    background-color: var(--brand-color, var(--roads-accent-color, #3b82f6));
  }
  ```
- If you need to compute derived colors, prefer using CSS color-mix or HSL adjustments within the theme layer.

Integrating custom brand styles
- Centralize brand styles using tokens:
  - --brand-color, --brand-contrast-color, --brand-font
- Apply brand tokens to common UI elements (header, buttons, inputs, etc.):
  ```css
  header { color: var(--brand-contrast-color); font-family: var(--brand-font, system-ui, sans-serif); }
  button.brand { background-color: var(--brand-color); color: white; border: 0; }
  input.brand { border-color: var(--brand-color); }
  ```
- If your map UI includes custom markers or SVGs, ensure those drawables reference tokens (e.g., stroke: var(--roads-road-color); fill: var(--roads-background-color)).
- Documentation tip: record the brand palette in docs/branding.md and link to this Theme Guide.

Validation tips
- Verify the tokens map to expected visuals on light theme (contrast, readability).
- Manually toggle the theme and inspect common UI areas: map controls, legend, search input, and Loja page.
- Accessibility: confirm color contrast for primary actions.

Notes and caveats
- This guide assumes a simple root-based theme switch. If your app uses a CSS-in-JS or CSS Modules, adapt the tokens in the corresponding layer but keep the same token names for consistency.
- When adding new tokens, update any documentation references to reflect their usage.
