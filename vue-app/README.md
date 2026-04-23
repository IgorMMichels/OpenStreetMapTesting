OpenStreetMap Testing - Vue.js Migration Skeleton

Overview:
- A minimal Vue 3 + Vite scaffold that renders a Leaflet map.
- Base layer defaults to a Roads Light style (CartoDB Positron).
- Satellite option is provided via a second base layer (Esri World Imagery).
- This is a starting point for componentization and gradual migration from static HTML to Vue components.

How to run (local development):
- Ensure Node.js is installed.
- Install dependencies: cd vue-app && npm install
- Start dev server: npm run dev
- Open http://localhost:5173/

Notes:
- Leaflet CSS is loaded from CDN in index.html for simplicity in this scaffold.
- The Vue app does not yet integrate with the existing static pages; this is a standalone migration surface.
