<script setup>
import { ref } from 'vue'
import axios from 'axios'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([])
const sortBy = ref('')
const searchQuery = ref('')

const getInfo = async () => {
  try {
    const { data } = await axios.get(`https://5fec76082414df5a.mokky.dev/items`, {
      params: {
        sortBy: sortBy.value,
        title: `*${searchQuery.value}*`
      }
    })
    items.value = data
  } catch (error) {
    console.error('Не удалось получить данные: ', error)
  }
}

const onChangeSort = (event) => {
  sortBy.value = event.target.value
  getInfo()
}

const onChangeSerch = (event) => {
  searchQuery.value = event.target.value
  getInfo()
}

getInfo()
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
            @change="onChangeSort"
            class="py-2 px-3 border rounded-md outline-none"
          >
            <option value="title">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>

          <div class="relative">
            <img
              class="absolute top-3 left-4 cursor-pointer"
              src="/search.svg"
              alt="Search"
            >
            <input
              @input="onChangeSerch"
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              type="text"
              placeholder="поиск..."
            >
          </div>
        </div>
      </div>

      <CardList :items="items" />
    </div>
  </div>
</template>
