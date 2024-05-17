<script setup>
import CharacterList from './components/CharacterList.vue'
import Filter from './components/Filter.vue'
import Pagination from './components/Pagination.vue'
import axios from 'axios'
import { ref, onMounted, reactive, provide } from 'vue'
import { BASE_URL } from './constant.js'

const items = ref([])
const info = ref([])
const filters = reactive({
  status: '',
  species: '',
})

const fetchData = async (url) => {
  try {
    const { data } = await axios.get(url)
    items.value = data.results
    info.value = data.info
    error = false
  } catch (err) {
    console.log(err)
  }
}

provide('fetching', {
  fetchData,
  filters,
})

onMounted(async () => {
  await fetchData(BASE_URL)
})
</script>

<template>
  <Pagination :info="info" />
  <Filter />
  <CharacterList :items="items" />
</template>
