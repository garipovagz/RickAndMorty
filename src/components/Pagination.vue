<script setup>
import { ref } from 'vue'

const currentPage = ref(1)

import { inject } from 'vue'

const props = defineProps({
  info: Object,
})

const { fetchData, filters } = inject('fetching')

const goToPage = (currentPage) => {
  fetchData(
    `https://rickandmortyapi.com/api/character/?status=${filters.status}&species=${filters.species}&page=${currentPage}`
  )
}
</script>

<template>
  <div>
    <vue-awesome-paginate
      :total-items="props.info.count"
      v-model="currentPage"
      @click="goToPage(currentPage)"
      :items-per-page="20"
      :max-pages-shown="10"
    >
      <template #prev-button>
        <span
          :disabled="props.info.prev == null"
          @click="fetchData(props.info.prev)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="white"
            width="12"
            height="12"
            viewBox="0 0 24 24"
          >
            <path d="M8.122 24l-4.122-4 8-8-8-8 4.122-4 11.878 12z" />
          </svg>
        </span>
      </template>

      <template #next-button>
        <span
          :disabled="props.info.next == null"
          @click="fetchData(props.info.next)"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="white"
            width="12"
            height="12"
            viewBox="0 0 24 24"
          >
            <path d="M8.122 24l-4.122-4 8-8-8-8 4.122-4 11.878 12z" />
          </svg>
        </span>
      </template>
    </vue-awesome-paginate>
  </div>
</template>

<style>
.pagination-container {
  margin: 20px 10px 10px;
  column-gap: 10px;
  align-items: center;
}
.paginate-buttons {
  height: 35px;
  width: 35px;
  cursor: pointer;
  border-radius: 4px;
  background-color: white;
  border: none;
  color: black;
}

.back-button,
.next-button {
  background-color: #c0c0c0;
  color: white;
  border-radius: 8px;
  height: 45px;
  width: 45px;
}
.active-page {
  background-color: rgb(0, 128, 128);
}
.paginate-buttons:hover {
  background-color: #778899;
}
.active-page:hover {
  background-color: rgb(0, 128, 128);
}

.back-button svg {
  transform: rotate(180deg) translateY(-2px);
}
.next-button svg {
  transform: translateY(2px);
}

.back-button:hover,
.next-button:hover {
  background-color: rgb(0, 128, 128);
}

.back-button:active,
.next-button:active {
  background-color: rgb(85, 85, 85);
}
</style>
