Title: Architecture overview for OpenStreetMapTesting (Vue migration)

Summary:
- Current app is a pair of static HTML pages using Leaflet for mapping.
- Migration plan introduces a new Vue 3 + Vite app to componentize UI and enable future enhancements.
- Core map component will encapsulate Leaflet initialization, theming (roads light vs satellite), and geolocation.

High-level components:
- MapView.vue: Leaflet map wrapper with base layers and layer control.
- App.vue: Simple container hosting MapView and header.
- Shared assets: Leaflet CSS via CDN in scaffold.

Data flow:
- Map tiles come from external tile services (OpenStreetMap roads, Esri satellite).
- Geolocation uses browser API to center the map.
- No server API calls in the current implementation; the Vue map consumes tile layers only.

Migration risks:
- Dependency availability (Leaflet, Carto tiles) and CSP if hosting on restricted domains.
- Migration footprint: keep existing static pages until Vue app is validated.
