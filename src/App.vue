<script setup>
import { onMounted, ref, reactive, watch } from 'vue'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'
import axios from 'axios'

const items = ref([])

const filters = reactive({
  sortBy: '',
  searchQuery: ''
})

const onChangeSearch = (e) => {
  filters.value.searchQuery = e.target.value
}

const onChangeSelect = (e) => {
  console.log(e.target.value)
  filters.sortBy = e.target.value
}

onMounted(async () => {
  try {
    const { data } = await axios.get('https://9f380676a5fecf90.mokky.dev/items')
    items.value = data
  } catch (error) {
    console.log(error)
  }
});

watch(filters, async () => {
  try {
    const { data } = await axios.get(
      `https://9f380676a5fecf90.mokky.dev/items?sortBy=${filters.sortBy}`
    )
    items.value = data
  } catch (error) {
    console.log(error)
  }
});


</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select
            @change="onChangeSelect"
            class="py-2 px-3 border rounded-md bg-white text-gray-400"
          >
            <option value="name">По Названию</option>
            <option value="price">По цене(возрастанию)</option>
            <option value="-price">По цене(убыванию)</option>
          </select>

          <div class="relative">
            <img src="/search.svg" class="absolute left-4 top-3" />
            <input
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              type="text"
              placeholder="Поиск..."
            />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
