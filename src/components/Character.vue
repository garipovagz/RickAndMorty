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
  <div class="container">
    <img :src="imageUrl" :alt="name" />
    <div class="info">
      <div>
        <h2>{{ name }}</h2>
        <div class="status">
          <svg v-show="status === 'Alive'">
            <circle cx="5" cy="5" r="5" fill="#32CD32" />
          </svg>
          <svg v-show="status === 'Dead'">
            <circle cx="5" cy="5" r="5" fill="#EF0A0A" />
          </svg>
          <svg v-show="status === 'unknown'">
            <circle cx="5" cy="5" r="5" fill="#A9A9A9" />
          </svg>
          <p>{{ status }} - {{ species }}</p>
        </div>
      </div>
      <div class="section">
        <p class="text-grey">Last known location:</p>
        <p>{{ location }}</p>
      </div>
      <div class="section">
        <p class="text-grey">First seen in:</p>
        <p>{{ location2 }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  margin: 20px;
  border-radius: 0.5rem;
  background-color: rgb(60, 62, 68);
  color: white;
}

@media (min-width: 870px) {
  .container {
    display: flex;
  }
}
img {
  border-radius: 0.5rem;
  width: 300px;
  height: 300px;
}

.info {
  padding: 20px;
}

svg {
  height: 10px;
  width: 10px;
}

.status p {
  display: inline;
  padding: 5px;
}

h2 {
  font-weight: 600;
}

.section {
  margin-top: 14px;
}

.text-grey {
  color: rgb(158, 158, 158);
  font-size: 20px;
  font-weight: 500;
}
</style>
