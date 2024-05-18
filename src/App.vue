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
  <div class="header"><Pagination :info="info" /> <Filter /></div>
  <CharacterList class="list" :items="items" />
</template>

<style scoped>
.header {
  background-color: grey;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 auto;
}

.list {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  gap: 0px 0px;
  grid-template-areas:
    '. . .'
    '. . .'
    '. . .'
    '. . .'
    '. . .'
    '. . .'
    '. . .';
  padding: 0 81px;
}
</style>
