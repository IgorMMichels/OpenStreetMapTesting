Vue.js migration scaffold for the OSM mapping project

- Provides a minimal Vue 3 + Vite app that reproduces the current Leaflet-based map with a satellite/streets toggle.
- Includes a Roads Light Theme ready for theming the UI.

How to use:
- Install: cd vue-migration && npm install
- Run dev: npm run dev
- Open: http://localhost:5173/

Notes:
- This is a separate frontend scaffold to de-risk migration before touching the existing static pages.
- The map itself uses Leaflet loaded via npm (leaflet) and CSS bundled by Vite.
