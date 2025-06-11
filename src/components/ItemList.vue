<template>
  <div class="item-list">
    <ItemButton
      v-for="item in items"
      :key="item.id"
      :item="item"
      :selected="isSelected(item)"
      @select="$emit('select', item)"
    />
  </div>
</template>

<script setup>
import ItemButton from './ItemButton.vue'

const props = defineProps({
  items: {
    type: Array,
    required: true
  },
  selected: {
    type: [Array, Object, Number, null],
    default: () => []
  },
  limit: {
    type: Number,
    default: null
  },
  multiple: {
    type: Boolean,
    default: false
  }
})


function isSelected(item) {
  if (props.multiple) {
    if (Array.isArray(props.selected)) {
      return props.selected.some(sel => sel.id === item.id)
    }
    return false
  } else {
    return props.selected && props.selected.id === item.id
  }
}
</script>

<style>
.item-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  border: 1px solid #000;
  padding: 10px;
  border-radius: 6px;

}
</style>
