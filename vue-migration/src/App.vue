<template>
  <div class="app">
    <header class="site-header roads-theme">
      <h1>OSM Map - Vue Migration</h1>
      <p>Leaflet-based map migrated to Vue with a satellite/streets toggle.</p>
    </header>
    <OSMMap />
  </div>
  </template>
<script setup lang="ts">
import OSMMap from './components/OSMMap.vue'
</script>
<style>
/* Roads Light Theme - basic global tokens */
:root {
  --bg: #ffffff;
  --text: #111;
  --primary: #667eea;
}
.roads-theme {
  background: var(--bg);
  color: var(--text);
}
.site-header {
  text-align: center;
  padding: 12px 16px;
}
</style>
