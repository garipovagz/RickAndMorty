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
  <div class="search">
    <input
      @input="filters.species = $event.target.value"
      type="text"
      placeholder="Species"
    />
    <select @change="filters.status = $event.target.value">
      <option value=" ">All</option>
      <option value="Alive">Alive</option>
      <option value="Dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button @click="filter">Применить</button>
  </div>
</template>

<style scoped>
.search {
  display: flex;
  column-gap: 20px;

  border-radius: 4px;
  cursor: pointer;
}

input,
button,
select {
  margin: 10px;
  cursor: pointer;
  height: 35px;
  font-size: 15px;
  font-family: 'Helvetica Neue', Helvetica, sans-serif;
}

option {
  background-color: rgb(0, 128, 128);
}

button:hover {
  background-color: rgb(0, 128, 128);
}
</style>
