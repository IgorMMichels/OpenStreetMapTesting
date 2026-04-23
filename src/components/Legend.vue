<template>
  <aside class="legend" aria-label="Map legend">
    <h4>Legend</h4>
    <ul>
      <li v-for="(item, idx) in items" :key="idx">
        <span class="swatch" :style="{ background: item.color }"></span>
        <span class="label">{{ item.label }}</span>
      </li>
    </ul>
  </aside>
  </template>

<script setup>
import { defineProps } from 'vue'

// Accept an array of legend items: [{ label, color }, ...]
const props = defineProps({ items: { type: Array, default: () => [] } })
</script>

<style scoped>
.legend {
  padding: 8px 12px;
  background: rgba(255,255,255,0.9);
  border: 1px solid #ddd;
  border-radius: 6px;
  position: absolute;
  right: 12px;
  top: 12px;
  min-width: 140px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
}
.legend h4 {
  margin: 0 0 8px 0;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
.legend ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.legend li {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  margin: 6px 0;
}
.swatch {
  width: 14px;
  height: 10px;
  display: inline-block;
  border-radius: 2px;
}
.label { color: #333; }
</style>
