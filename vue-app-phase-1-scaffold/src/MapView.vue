<template>
  <div class="map-wrapper" style="height:400px; width:100%; position: relative;">
    <div id="map" style="height:100%; width:100%;"></div>

    <!-- UI overlays: theme toggle, search, and legend -->
    <div class="map-ui" style="position:absolute; top:8px; left:8px; right:8px; display:flex; flex-direction:column; gap:8px; pointer-events:none;">
      <div class="controls-panel" style="display:flex; gap:8px; align-items:center; background: rgba(255,255,255,0.95); padding:6px; border-radius:6px; width: max-content; align-self:flex-start; pointer-events:auto;">
        <button @click="toggleBase" title="Toggle theme" style="padding:6px 10px;">Toggle Theme</button>
        <div class="search-bar" style="display:flex; align-items:center;">
          <input v-model="query" @keyup.enter="performSearch" placeholder="Search location" style="width:180px; padding:4px 6px; border:1px solid #ccc; border-radius:4px;" />
          <button @click="performSearch" style="margin-left:6px; padding:6px 8px;">Search</button>
        </div>
      </div>
      <div class="legend" style="align-self:flex-start; background: rgba(255,255,255,0.95); padding:6px 8px; border-radius:6px; font-size:12px;">
        <strong>Legend</strong><br/>Roads Light vs Satellite
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'

const mapEl = ref(null)
const query = ref('')
let roadsLight
let satellite
let baseLayers = {}

const performSearch = async () => {
  const q = (query.value || '').trim()
  if (!q) return
  const url = `https://nominatim.openstreetmap.org/search?q=${encodeURIComponent(q)}&format=json&limit=5`
  try {
    const resp = await fetch(url, { headers: { 'Accept': 'application/json' } })
    const results = await resp.json()
    if (results && results.length > 0) {
      const lat = parseFloat(results[0].lat)
      const lon = parseFloat(results[0].lon)
      mapEl.value.setView([lat, lon], 14)
      L.marker([lat, lon]).addTo(mapEl.value).bindPopup(results[0].display_name).openPopup()
    } else {
      alert('Location not found')
    }
  } catch (e) {
    console.error(e)
  }
}

const toggleBase = () => {
  if (!mapEl.value) return
  if (mapEl.value.hasLayer(roadsLight)) {
    mapEl.value.removeLayer(roadsLight)
    satellite.addTo(mapEl.value)
  } else if (mapEl.value.hasLayer(satellite)) {
    mapEl.value.removeLayer(satellite)
    roadsLight.addTo(mapEl.value)
  } else {
    roadsLight.addTo(mapEl.value)
  }
}

onMounted(() => {
  roadsLight = L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
    attribution: '&copy; OpenStreetMap contributors, &copy; CARTO',
    maxZoom: 19
  })

  satellite = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
    attribution: 'Tiles © Esri'
  })

  mapEl.value = L.map('map', {
    center: [0, 0],
    zoom: 2,
    zoomControl: true,
  })

  baseLayers = {
    'Roads Light': roadsLight,
    'Satellite': satellite
  }

  roadsLight.addTo(mapEl.value)
  L.control.layers(baseLayers).addTo(mapEl.value)

  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition((pos) => {
      const lat = pos.coords.latitude
      const lon = pos.coords.longitude
      mapEl.value.setView([lat, lon], 12)
      L.marker([lat, lon]).addTo(mapEl.value).bindPopup('You are here').openPopup()
    }, () => {
      mapEl.value.setView([51.505, -0.09], 13)
    })
  } else {
    mapEl.value.setView([51.505, -0.09], 13)
  }
})
</script>

<style scoped>
#map { height: 400px; }
.map-wrapper { height: 400px; width: 100%; position: relative; }
.map-ui { position: absolute; top: 0; left: 0; right: 0; bottom: 0; pointer-events: none; }
.controls-panel { display: flex; gap: 8px; align-items: center; background: rgba(255,255,255,0.95); padding: 6px; border-radius: 6px; width: max-content; margin: 8px; pointer-events: auto; }
.legend { background: rgba(255,255,255,0.95); padding: 6px 8px; border-radius: 6px; font-size: 12px; margin-left: 8px; }
.search-bar input { width: 180px; padding: 4px 6px; border: 1px solid #ccc; border-radius: 4px; }
</style>
