# Implementation Plan: Vue 3 + Vite Migration for Leaflet Map

This plan outlines the concrete steps to implement the Vue-based, componentized map application with Leaflet, roads-light theming, and Loja route integration. It is structured as a sequence of phases with concrete tasks, deliverables, and acceptance criteria.

## Phase 1 – Project Scaffolding
- Create Vue 3 + Vite project skeleton
- Configure Vue Router with routes for MapView and Loja (storefront)
- Establish folder structure: src/components, src/views, src/assets, src/router
- Deliverable: a runnable Vue app shell with two routes and a basic layout

## Phase 2 – Map Componentization (Leaflet)
- Implement MapView.vue as a reusable Leaflet wrapper
- Abstract map initialization, center/zoom props, and events (move, zoom, click)
- Integrate roads-light tile layer (initial token: ROAD_LIGHT_TILE_URL)
- Ensure geolocation compatibility via a GeolocationControl in MapControls
- Deliverable: MapView component that can be dropped into any Vue view

## Phase 3 – Roads Light Theme System
- Define CSS variables for theme tokens in a dedicated theme file (themes/roads-light.css)
- Apply tokens to app layout and controls
- Implement a toggle to switch themes if needed in future (start with single roads-light theme)
- Deliverable: Theming ready to swap with minimal code changes

## Phase 4 – Enhanced UI Components
- Sidebar component with collapsible sections: layers, search, info
- MapControls component: zoom, pan, fitBounds
- InfoPanel component: displays selected feature information or current map state
- Deliverable: UI kit for map page with reusable components

## Phase 5 – Loja Route Integration
- Create LojaView.vue with a basic storefront layout and routing anchor points from the map
- Wire navigation between MapView and Loja routes; ensure location context flows if needed
- Deliverable: functional Loja route with coherent header/navigation

## Phase 6 – Documentation
- Update README with setup, run, and build instructions
- Add a dedicated docs folder with design_doc.md and implementation_plan.md (this file)
- Deliverable: comprehensive docs for developers and future contributors

## Phase 7 – Theme Customization Documentation
- Add a Theme Customization section detailing how to switch tile providers and adjust CSS variables
- Provide examples for road-style and color schemes
- Deliverable: Theme customization guide in docs

## Validation Strategy
- Local run: npm install; npm run dev; verify MapView renders and geolocation works
- Route navigation: ensure /map and /loja routes render without errors
- Lint/TypeScript checks pass; basic UI responsiveness checks across screen sizes
- Accessibility checks: keyboard navigation and focus states

## Risks and Contingencies
- Risk: Tile URL changes affect map visuals. Contingency: keep a fallback tile URL and a feature flag to switch tiles
- Risk: Loja page scaffolding delays progress. Contingency: keep Loja route minimal and incrementally enhance

## Timeline (Recommended)
- Week 1: Phase 1 and Phase 2 completion
- Week 2: Phase 3 + Phase 4; Phase 5 skeleton
- Week 3: Phase 5 completion + Phase 6; Phase 7 draft
- Week 4: Final polish, verification, and documentation packaging

## Deliverables Summary
- Vue 3 + Vite project scaffold
- MapView component with Leaflet integration and roads-light theme
- UI components: Sidebar, MapControls, InfoPanel
- Loja route skeleton integrated with routing
- Documentation: design_doc.md and implementation_plan.md; updated README
