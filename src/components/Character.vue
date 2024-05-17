<script setup>
import axios from 'axios'
import { ref } from 'vue'
const props = defineProps({
  id: Number,
  name: String,
  status: String,
  species: String,
  imageUrl: String,
  location: String,
  firstEpisode: String,
})

const location2 = ref('')
const fetchData = async () => {
  try {
    const { data } = await axios.get(props.firstEpisode)
    location2.value = data.name
  } catch (err) {
    console.log(err)
  }
}
fetchData()
</script>

<template>
  <div class="section">
    <img :src="imageUrl" :alt="name" />
    <div class="info">
      <div>
        <p>{{ name }}</p>
        <p>{{ status }} - {{ species }}</p>
      </div>
      <div>
        <p>Last known location:</p>
        <p>{{ location }}</p>
      </div>
      <div>
        <p>First seen in:</p>
        <p>{{ location2 }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
img {
  width: 100%;
}
.section {
  flex-direction: column;
  height: initial;
  width: 100%;
  margin: 0.75rem;
  border-radius: 0.5rem;
  background-color: rgb(60, 62, 68);
  color: white;
}

.info {
  padding: 10px;
}
</style>
