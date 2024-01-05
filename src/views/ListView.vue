<script setup lang="ts">
import ListVue from '../components/List.vue'
import type { Movie } from '../types/types'
import { onMounted, ref } from 'vue'
import axios from 'axios'

const movies = ref<Movie[]>([])

const getMovies = async () => {
  try {
    const response = await axios.get('http://localhost:3000/movies')
    movies.value = response.data
  } catch (e) {
    console.log(e)
  }
}

getMovies();

</script>

<template>
  <div class="wrapper list">
    <ListVue :movies="movies"></ListVue>
  </div>
</template>

<style>

.list {
  flex-direction: column;
}

</style>
