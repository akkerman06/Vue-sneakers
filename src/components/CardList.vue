<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,
  addToFavorite: Function
})
const emit = defineEmits(['addToFavorite'])

const onClickAdd = () => {
  emit('addToFavorite')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :id="item.id"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :onClickAdd="onClickAdd"
      :onClickFavorite="() => emit('addToFavorite', item)"
      :isFavorite="item.isFavorite"
    />
  </div>
</template>
