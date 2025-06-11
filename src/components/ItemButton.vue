<template>
  <button :class="['item-button', { selected }]" @click="$emit('select')">
    {{ item.name }}
  </button>
</template>

<script setup>
defineProps({
  item: {
    type: Object,
    required: true
  },
  selected: {
    type: Boolean,
    default: false
  }
})
</script>

<style>
.item-button {
  padding: 8px 16px;
  margin: 4px;
  border: 1px solid #aaa;
  background: #f8f8f8;
  cursor: pointer;
  transition: background 0.2s;
  border-radius: 6px;
}
.item-button.selected {
  background: #aee1ff;
  border-color: #2196f3;
  color: #00395c;
}
</style>
