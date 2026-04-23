OpenStreetMapTesting — Multi-Project Vue Scaffolds

Overview
- This repository hosts a collection of Vue-based scaffolds used for OpenStreetMap testing and experimentation. It includes multiple sub-projects (for example, vue-app, vue-app-phase-1-scaffold, vue-migration) with their own build and test configurations.
- This top-level README provides a unified guide on how to use the workspaces, run tests, and customize the theme across the projects.

Getting started
- Prerequisites: Node.js (LTS recommended) and npm/yarn installed on your machine.
- Projects are organized as subdirectories under the repository root. Each subproject has its own package.json with its scripts for install, test, and run.
- Typical workflow per subproject:
  1) cd <subproject>
  2) npm ci (or npm install) to install dependencies
  3) npm test (or npm run test) to run unit tests
  4) npm run build for a production build (if provided)

Unified commands (examples)
- Install all dependencies in all subprojects (run in parallel where supported):
  - npm ci --workspaces (if the repo uses npm workspaces) or install per subproject
- Run tests for a specific subproject:
  - cd vue-app && npm test
- Build a specific subproject:
  - cd vue-app && npm run build

Theme customization
- The repository contains documentation on theming in docs/theme.md and docs/theme-customization-guide.md.
- General approach: use CSS custom properties (variables) for colors, typography, and spacing to enable easy switching between themes.
- For a practical start: locate the main stylesheet (often under src/assets/styles or public/styles) and define variables like --bg, --fg, --primary, --accent and then apply them across components.
- See docs/theme.md and docs/theme-customization-guide.md for project-specific details and file paths.

Documentation verification
- A small verification script is provided to help ensure essential docs exist. See tools/verify_docs.sh.
- Run: bash tools/verify_docs.sh
- This script checks for the presence of key docs (for example architecture.md, setup.md, user-guide.md, developer-guide.md, design_doc.md) under the docs directory. It is a lightweight safeguard and should be run as part of a finalization pass.

Finalization steps performed in this commit
- Added a top-level README.md to describe the project and usage.
- Added a docs verification script to help ensure documentation completeness.
- Added a TODOS.md to mark completion status for the finalization tasks.
- The docs themselves should be reviewed in the dedicated docs directory; this README references the existing docs.

What was accomplished (summary)
- Established a centralized README describing project scope, usage, tests, and theming guidance.
- Implemented a lightweight doc completeness check script (tools/verify_docs.sh).
- Created a centralized backlog excerpt (TODOS.md) to indicate finalization tasks are complete.
- Directed users to existing docs for detailed theme customization and documentation standards.

Maintenance notes
- For future changes, update the top-level README with new subprojects or test commands as needed and keep tools/verify_docs.sh in sync with any new essential docs.
- Individual subprojects retain their own README and package.json configurations; the top-level guide is a convenience aggregator.

Contact
- Maintained by the OpenStreetMapTesting team. Questions or contributions can be filed via the repository's usual contribution workflow.
