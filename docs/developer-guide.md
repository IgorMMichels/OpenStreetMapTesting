# Vue App Developer Guide

This guide helps developers extend, customize, and contribute to the Vue application.

## Project Structure (typical)
- src/           - Source files
- src/assets/    - Images, fonts, styles
- src/components/ - Reusable UI components
- src/views/      - Page-level components
- src/router/     - Route configuration
- src/store/      - State management (Vuex/Pinia)
- tests/          - Unit and integration tests
- public/         - Static assets

## Setup & Tools
- Install dependencies: npm install
- Run in development: npm run dev
- Lint: npm run lint
- Type-check (if using TypeScript): npm run typecheck
- Tests: npm test (or npm run test:unit / test:e2e as configured)

## Contributing
- Follow the project’s code style and commit conventions.
- Before submitting a PR, ensure tests pass and lint is clean.
- Use small, focused commits with meaningful messages.

## Extending the App
- Creating a new component: add to src/components, import in a view, and export for reuse.
- Adding routes: modify src/router/index.js (or equivalent) and ensure lazy-loading where appropriate.
- State management: extend store modules; keep selectors/getters pure.
- Styling: use the existing theming system; add CSS variables if needed.

## Testing & Quality
- Unit tests for components and utilities.
- End-to-end tests for critical flows (login, navigation, data entry).
- Run tests locally before pushing changes.
