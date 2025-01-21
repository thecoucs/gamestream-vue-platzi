<script setup>
import LayoutHero from './components/Layout/LayoutHero.vue'
import GameCard from './components/Games/GameCard.vue'
import GameLayout from './components/Games/GameLayout.vue'
import { onMounted, reactive } from 'vue'

const API_URL = 'https://gamestreamapi.herokuapp.com/api/games'

const state = reactive({
  error: null,
  isLoading: false,
  data: [],
})

const fetchGames = async () => {
  try {
    state.isLoading = true
    const response = await fetch(API_URL)
    const json = await response.json()
    state.data = json
  } catch (error) {
    console.error(error)
    state.error = error
  } finally {
    state.isLoading = false
  }
}

onMounted(() => {
  fetchGames()
})
</script>

<template>
  <LayoutHero />
  <GameLayout>

    <GameCard v-for="game in state.data" :key="game.title" :game="game"/>
  </GameLayout>
  <main></main>
</template>

<style scoped>
main {
  padding: 2rem;
}
</style>
