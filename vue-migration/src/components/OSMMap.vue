<template>
  <div class="osm-map-wrapper">
    <div id="map" ref="mapEl" style="height:92vh; width:100%;"></div>
    <button class="toggle-sat" @click="toggleSatellite">{{ satellite ? 'Ruas' : 'Satelite' }}</button>
  </div>
  </template>
<script lang="ts" setup>
import { onMounted, ref } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

const mapEl = ref<HTMLElement | null>(null)
let map: L.Map
let tiles: L.TileLayer | undefined
const satellite = ref(false)

function loadTiles(type: 'streets'|'satellite') {
  if (tiles) map.removeLayer(tiles)
  if (type === 'satellite') {
    tiles = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
      maxZoom: 18,
      attribution: 'Esri'
    })
  } else {
    tiles = L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
      maxZoom: 18,
      attribution: 'OSM'
    })
  }
  tiles.addTo(map)
}

function toggleSatellite() {
  satellite.value = !satellite.value
  loadTiles(satellite.value ? 'satellite' : 'streets')
}

function initView(lat: number, lon: number) {
  map.setView([lat, lon], 15)
  loadTiles('streets')
  L.marker([lat, lon]).addTo(map).bindPopup('<div style="text-align:center; padding:8px;">Loja Teste</div>')
}

onMounted(() => {
  map = L.map('map')
  // Try geolocation; fallback to Joinville coordinates from original project
  const fallback = { lat: -26.3039, lon: -48.8458 }
  if ('geolocation' in navigator) {
    navigator.geolocation.getCurrentPosition(
      (p) => initView(p.coords.latitude, p.coords.longitude),
      () => initView(fallback.lat, fallback.lon),
      { enableHighAccuracy: false, timeout: 5000 }
    )
  } else {
    initView(fallback.lat, fallback.lon)
  }
})
</script>
<style scoped>
.osm-map-wrapper { position: relative; }
.toggle-sat {
  position: absolute; top: 10px; right: 10px; z-index: 1000;
  padding: 8px 12px; border: none; background: white; border-radius: 6px; cursor: pointer;
}
</style>
