# Design Document: Vue 3 + Vite Migration for Leaflet Map

This document defines the architectural and UI design for migrating the current static Leaflet map application into a Vue 3 + Vite project, with a componentized structure and a roads-light theme. The migration will preserve core map and geolocation functionality while introducing a reusable map component, enhanced UI, and a Vue-based storefront route integration.

## Goals
- Migrate from a static Leaflet map to a Vue 3 + Vite application with a clean, componentized architecture.
- Replace the satellite-only map theme with a roads light themed map via CSS variables and Leaflet tile layers.
- Implement a reusable Leaflet map component and compose it with additional UI components (sidebar, controls, info panels).
- Integrate the existing loja storefront page into the Vue app via routing, preserving navigation semantics.
- Create comprehensive documentation and a theme customization guide.

## Architecture Overview
- Tech stack: Vue 3, Vite, Vue Router, Leaflet, and CSS for theming.
- Project structure: a dedicated components folder for MapView, Sidebar, MapControls, and Loja integration components; a routes configuration for Map and Loja pages; a shared assets folder for themes.
- Data flow: the MapView component exposes events and accepts props for center, zoom, and tile layer; parent components manage state and trigger map updates. Loja page is a separate route/component that can exchange minimal props if needed (e.g., current location).

## Theme System (Roads Light)
- Implement theme via CSS variables (colors, typography, elevations) and a dedicated roads-light tile layer URL for Leaflet.
- Example tokens: --bg, --surface, --text, --muted, --accent, --tile-url.
- Tile layers: switch from satellite tile URL to a roads-focused light tile layer (e.g., using a public tile source) with a graceful fallback.

## Components
- MapView.vue: Lightweight Leaflet wrapper that renders the map and exposes events (move, zoom, click) and props for center/zoom/tile layer.
- Sidebar.vue: Collapsible panel showing map layers, search, and quick actions.
- MapControls.vue: Zoom, pan, and theme toggle controls.
- LojaView.vue: Basic storefront view integrated via Vue Router; designed to be swapped with a full storefront as needed.
- Header.vue / Layout.vue: Global layout and theming toggle (if desired) with accessibility considerations.

## Data Flows and API
- MapView props: center: [lat, lng], zoom: number, tileLayer: string (URL template).
- MapView emits: update:center, update:zoom, mapReady.
- LojaView may receive initial location context and expose navigation actions back to the map when needed.

## Migration Plan (High-Level)
- Phase 1: Scaffold Vue 3 + Vite project structure and routing for Map and Loja pages.
- Phase 2: Implement MapView component with Leaflet integration and roads-light theme tokens.
- Phase 3: Build UI components (Sidebar, MapControls) and compose the page layout.
- Phase 4: Integrate Loja route and ensure navigation between map and storefront is coherent.
- Phase 5: Create comprehensive documentation and a theme customization guide.
- Phase 6: Validation and polish: lint, type checks, lightweight tests, and manual QA.

## Accessibility and UX Considerations
- Ensure color contrast for UI components and map overlays.
- Keyboard navigation for map controls and sidebar interactions.
- Clear focus states and ARIA labeling for map controls.

## Risks and Mitigations
- Risk: Tile source changes affect map rendering. Mitigation: implement a robust fallback tile URL and feature flag to revert if needed.
- Risk: Porting geolocation logic to Vue may introduce race conditions. Mitigation: centralize geolocation state in a parent component and debounce events.
- Risk: Loja integration delays blocking the plan. Mitigation: implement routing skeleton first and fill Loja progressively.

## Acceptance Criteria
- A working Vue 3 + Vite app with a MapView component that renders a roads-light Leaflet map.
- Routes for Map and Loja pages function correctly, with navigation between pages.
- The design is documented, and a theme customization guide is present.
- Linting and type checks pass; basic manual QA confirms UI responsiveness and accessibility basics.

## Appendix: References
- Leaflet integration patterns with Vue 3
- CSS variables theming approaches
- Vue Router setup examples
