<template>
  <div class="controls-panel" aria-label="Map controls">
    <button @click="emitZoomIn">+</button>
    <button @click="emitZoomOut">-</button>
    <button @click="emitReset">Reset</button>
  </div>
  </template>

<script setup>
import { defineEmits } from 'vue'
const emits = defineEmits(['zoom-in', 'zoom-out', 'reset'])

function emitZoomIn() { emits('zoom-in') }
function emitZoomOut() { emits('zoom-out') }
function emitReset() { emits('reset') }
</script>

<style scoped>
.controls-panel {
  display: flex;
  gap: 6px;
  position: absolute;
  left: 12px;
  bottom: 12px;
  background: rgba(255,255,255,0.95);
  padding: 6px;
  border-radius: 6px;
  border: 1px solid #ddd;
}
.controls-panel button {
  width: 32px; height: 32px; border-radius: 6px; border: none; cursor: pointer;
  background: #fff; box-shadow: 0 1px 2px rgba(0,0,0,0.08);
}
</style>
