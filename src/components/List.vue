<script setup lang="ts">
import { ref, type PropType, computed } from 'vue'
import type { Movie } from '../types/types'

const props = defineProps({
  movies: {
    type: Array as PropType<Movie[]>,
    required: true
  }
})

type MovieKeys = 'title' | 'director' | 'releaseYear' | 'imdbRating' | 'income'
type sortItem = {
  title: string
  sortTitle: MovieKeys
  value: 1 | -1
}

const currentSort = ref<MovieKeys>('title')
const currentSortDir = ref<1 | -1>(1)
const sortObject = ref<sortItem>({
  title: 'title up',
  sortTitle: 'title',
  value: 1
})

const sort = (s: sortItem) => {
  currentSort.value = s.sortTitle
  currentSortDir.value = s.value
}

const sortedMovies = computed(() => {
  return [...props.movies].sort((a, b) => {
    if (a[currentSort.value] < b[currentSort.value]) return -1 * currentSortDir.value
    if (a[currentSort.value] > b[currentSort.value]) return 1 * currentSortDir.value
    return 0
  })
})
const sortOptions: Array<sortItem> = [
  {
    title: 'title up',
    sortTitle: 'title',
    value: 1
  },
  {
    title: 'title down',
    sortTitle: 'title',
    value: -1
  },
  {
    title: 'Year up',
    sortTitle: 'releaseYear',
    value: 1
  },
  {
    title: 'Year down',
    sortTitle: 'releaseYear',
    value: -1
  },
  {
    title: 'Rating up',
    sortTitle: 'imdbRating',
    value: 1
  },
  {
    title: 'Rating down',
    sortTitle: 'imdbRating',
    value: -1
  }
]
</script>

<template>
  <div>
    <div class="row head">
      <select @change="sort(sortObject)" v-model="sortObject">
        <option v-for="option in sortOptions" :value="option">{{ option.title }}</option>
      </select>
    </div>
  </div>
  <div class="table">
    <div class="row item" v-for="movie in sortedMovies" :key="movie.id">
      <div class="title">{{ movie.title }}</div>
      <div>
        <div class="director">{{ movie.director }}</div>
        <div class="actors">
          <div v-for="actor in movie.actors">
            {{ actor }}
          </div>
        </div>
      </div>
      <div>
        <div class="year">{{ movie.releaseYear }}</div>
        <div class="income">{{ movie.income }}</div>
      </div>
      <div class="rating">{{ movie.imdbRating }}</div>
    </div>
  </div>
</template>

<style>
.table {
  display: flex;
  flex-direction: column;
  height: 210px;
  overflow-x: scroll;
  font-size: 20px;
}

.row {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 10px;
  padding: 10px;
}
@media (max-width: 600px) {
  .row {
    flex-direction: column;
    align-items: start;
  }
}

.head {
  font-family: Resist Bold;
  margin-bottom: 10px;
}

.year,
.rating {
  width: 65px;
}

.income {
  width: 100px;
}

.title,
.rating {
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
  font-family: Resist Bold;
  font-size: 25px;
}

.actors {
  display: flex;
  flex-direction: row;
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
}

.title,
.director {
  width: 300px;
}
</style>
