<script setup>
import Card from './Card.vue'

defineProps({
  items: Array,


})

const onClickAdd = () => {
  alert('В корзине')
}

const onClickFavorite = () => {
  alert('В избранном')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card :image-url="'/sneakers/sneakers-1.jpg'" :price="1200" :title="'Кроссовки мужские Nike'" :is-favorite="true"
      :is-added="true" :onClickAdd="onClickAdd" :onClickFavorite="onClickFavorite" />
  </div>
</template>
