<template>
  <div class="search-box" role="search" aria-label="Map search">
    <input
      v-model="query"
      @keyup.enter="onSearch"
      placeholder="Search map features..."
      aria-label="Search map"
    />
    <button @click="onSearch" aria-label="Search">Search</button>
  </div>
  </template>

<script setup>
import { defineEmits, ref } from 'vue'

const emits = defineEmits(['search'])
const query = ref('')

function onSearch() {
  emits('search', query.value)
}
</script>

<style scoped>
.search-box {
  display: flex;
  gap: 6px;
  align-items: center;
  padding: 6px;
  background: rgba(255,255,255,0.95);
  border: 1px solid #ddd;
  border-radius: 6px;
}
.search-box input {
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 6px 8px;
  min-width: 180px;
}
.search-box button {
  padding: 6px 10px;
  border: none;
  border-radius: 4px;
  background: #4f46e5;
  color: white;
  cursor: pointer;
}
.search-box button:hover { opacity: 0.92; }
</style>
