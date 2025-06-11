<template>
  <div class="selected-item-block">
    <template v-if="item">
      <div class="selected-item">{{ item.name }}</div>
    </template>
    <template v-else>
      <div class="placeholder">Выберите одну вещь справа внизу</div>
    </template>
  </div>
</template>

<script setup>
defineProps({
  item: {
    type: [Object, null],
    default: null
  }
})
</script>

<style>
.selected-item-block {
  min-height: 40px;
  border: 1px solid #000;
  padding: 12px;
  border-radius: 6px;
  background: #fff;
}

.placeholder {
  color: #aaa;
  font-style: italic;
}
</style>
