<script setup>
import axios from 'axios'
import { ref, onMounted, inject } from 'vue'
import CardList from '../components/CardList.vue'
const { addToCart, removeFromCart } = inject('cart')

const favorites = ref([])
const onClickAddPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}
onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://e8fbbfbfb79ac194.mokky.dev/favorites?_relations=items'
    )
    favorites.value = data.map((obj) => obj.item)
  } catch (e) {
    console.log(e)
  }
})
</script>

<template>
  <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>

  <CardList :items="favorites" is-favorites @add-to-cart="onClickAddPlus" />
</template>
