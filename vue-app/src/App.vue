<template>
  <div>
    <header>
      <strong>OpenStreetMap Testing</strong> · Vue.js migration scaffold
    </header>
    <main>
      <MapView />
    </main>
  </div>
</template>

<script>
import MapView from './components/MapView.vue'
export default {
  name: 'App',
  components: {
    MapView
  }
}
</script>

<style>
/* Global styles for the Vue app can live here if needed */
</style>
