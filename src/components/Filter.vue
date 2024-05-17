<script setup>
import { inject } from 'vue'

const { fetchData, filters } = inject('fetching')

const filter = () => {
  fetchData(
    `https://rickandmortyapi.com/api/character/?status=${filters.status}&species=${filters.species}`
  )
}
</script>
<template>
  <div>
    <input @input="filters.species = $event.target.value" type="text" />
    <select @change="filters.status = $event.target.value">
      <option value=" ">all</option>
      <option value="Alive">Alive</option>
      <option value="Dead">Dead</option>
      <option value="unknown">unknown</option>
    </select>
    <button @click="filter">Применить</button>
  </div>
</template>
