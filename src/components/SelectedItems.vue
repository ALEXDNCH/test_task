<template>
  <div class="selected-items">
    <template v-if="items && items.length">
      <div v-for="item in items" :key="item.id" class="selected-item">
        {{ item.name }}
      </div>
    </template>
    <template v-else>
      <div class="placeholder">Выберите 1–{{ LIMIT_ITEMS }} вещей ниже</div>
    </template>
  </div>
</template>

<script setup>
import { LIMIT_ITEMS } from '../app_settings'
defineProps({
  items: {
    type: Array,
    default: () => []
  }
})
</script>

<style>
.selected-items {
  min-height: 40px;
  border: 1px solid #000;
  padding: 12px;
  border-radius: 6px;
  background: #fff;
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
.selected-item {
  background: #e3f2fd;
  border: 1px solid #90caf9;
  border-radius: 3px;
  padding: 5px 10px;
  font-size: 14px;
}

.placeholder {
  color: #aaa;
  font-style: italic;
}
</style>
