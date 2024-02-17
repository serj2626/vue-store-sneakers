<script setup>

import Card from './Card.vue'

defineProps({
  items: Array
});

const onClickAdd = () => {
  alert('В корзине')
};

const onClickFavorite = () => {
  alert('В избранном')
};
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
    v-for="item in items" :key="item.id"
      :image-url="item.imageUrl"
      :price= item.price
      :title= item.title
      :is-favorite="true"
      :is-added="true"
      :onClickAdd="onClickAdd"
      :onClickFavorite="onClickFavorite"
    />
  </div>
</template>
