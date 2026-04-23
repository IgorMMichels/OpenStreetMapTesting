<template>
  <div class="map-light-theme">
    <!-- This is a lightweight wrapper to apply light-theme styling around the existing map. -->
    <slot></slot>
  </div>
  </template>

<script setup>
// No runtime logic yet. This wrapper enables phased integration of a light theme.
</script>

<style scoped>
/* Light theme tokens. These are intended to be consumed by the inner Map component or its children. */
.map-light-theme {
  --bg-color: #f7f7f7;
  --road-color: #e0e0e0;
  --text-color: #1f2937;
}
</style>
