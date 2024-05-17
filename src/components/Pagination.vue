<script setup>
import { inject } from 'vue'

const props = defineProps({
  info: Object,
})

const { fetchData, filters } = inject('fetching')

const goToPage = (p) => {
  fetchData(
    `https://rickandmortyapi.com/api/character/?status=${filters.status}&species=${filters.species}&page=${p}`
  )
}
</script>

<template>
  <button
    :disabled="props.info.prev == null"
    @click="fetchData(props.info.prev)"
  >
    Предыдущая
  </button>
  <button @click="goToPage(p)" v-for="p in props.info.pages" :key="p">
    {{ p }}
  </button>

  <button
    :disabled="props.info.next == null"
    @click="fetchData(props.info.next)"
  >
    Следующая
  </button>
</template>
