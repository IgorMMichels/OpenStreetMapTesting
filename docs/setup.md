Setup guide for OpenStreetMapTesting migration to Vue

- Prerequisites: Node.js (>=14), npm or yarn
- Folder layout:
  - Current app: index.html, loja/index.html, readme.MD
  - New app: vue-app/ (Vue 3 + Vite scaffold)

- Steps:
  1) Install dependencies: cd vue-app && npm install
  2) Run dev server: npm run dev
  3) Access: http://localhost:5173/

- Integration plan:
  - Do not replace existing static pages yet; run Vue app in parallel.
  - Later, consider routing to switch between static pages and Vue-driven map.
