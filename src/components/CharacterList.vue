<script setup>
import Character from './Character.vue'

defineProps({
  items: Array,
})
</script>

<template>
  <div class="list-wrapper">
    <Character
      v-for="item in items"
      :key="item.id"
      :imageUrl="item.image"
      :name="item.name"
      :status="item.status"
      :species="item.species"
      :location="item.location.name"
      :firstEpisode="item.episode[0]"
    />
  </div>
</template>

<style scoped>
.list-wrapper {
  display: grid;
  grid-template-columns: 1fr;
  padding: 0 100px;
}

@media (min-width: 1300px) {
  .list-wrapper {
    grid-template-columns: 1fr 1fr;
    padding: 0 80px;
  }
}

@media (min-width: 1880px) {
  .list-wrapper {
    grid-template-columns: 1fr 1fr 1fr;
    padding: 0 30px;
  }
}
</style>
