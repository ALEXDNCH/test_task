<template>
  <div class="main-wrapper">
    <div class="top-blocks">
      <div class="top-block left">
        <SelectedItems :items="selectedUserItems" />
      </div>
      <div class="top-block right">
        <SelectedItem :item="selectedChoiceItem" />
      </div>
    </div>

    <div class="bottom-blocks">
      <div class="bottom-block left">
        <h3>Вещи у пользователя</h3>
        <ItemList
          :items="userItems"
          :selected="selectedUserItems"
          :multiple="true"
          :limit="LIMIT_ITEMS"
          @select="handleUserItemSelect"
        />
      </div>
      <div class="bottom-block right">
        <h3>Вещи на выбор</h3>
        <ItemList
          :items="choiceItems"
          :selected="selectedChoiceItem"
          :multiple="false"
          @select="handleChoiceItemSelect"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import SelectedItems from './components/SelectedItems.vue'
import SelectedItem from './components/SelectedItem.vue'
import ItemList from './components/ItemList.vue'
import { getLocalStorage, setLocalStorage } from './utils/localStorage'
import userItems from "./userItems.json"
import choiceItems from "./choiceItems.json"
import { USER_ITEMS_KEY, CHOICE_ITEM_KEY, LIMIT_ITEMS } from './app_settings'



const selectedUserItems = ref(getLocalStorage(USER_ITEMS_KEY) ?? [])
const selectedChoiceItem = ref(getLocalStorage(CHOICE_ITEM_KEY) ?? null)

watch(selectedUserItems, (newVal) => setLocalStorage(USER_ITEMS_KEY, newVal), { deep: true })
watch(selectedChoiceItem, (newVal) => setLocalStorage(CHOICE_ITEM_KEY, newVal))

function handleUserItemSelect(item) {
  const idx = selectedUserItems.value.findIndex(i => i.id === item.id)
  if (idx !== -1) {
    selectedUserItems.value.splice(idx, 1)
  } else if (selectedUserItems.value.length < LIMIT_ITEMS) {
    selectedUserItems.value.push(item)
  }
}

function handleChoiceItemSelect(item) {
  if (selectedChoiceItem.value && selectedChoiceItem.value.id === item.id) {
    selectedChoiceItem.value = null
  } else {
    selectedChoiceItem.value = item
  }
}
</script>

<style>
.main-wrapper {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}
.top-blocks, .bottom-blocks {
  display: flex;
  gap: 24px;
}
.top-block, .bottom-block {
  flex: 1;
}
h3 {
  margin-bottom: 12px;
}
</style>
