<script setup>
import { useSlots } from 'vue'

const slots = useSlots()

</script>

<template>
  <section>
    <slot name="title" />
    <h2 v-if="slots.title === undefined">Recent games</h2>
    <div class="game-layout">
      <slot />
    </div>
  </section>
</template>

<style scoped>
.game-layout {
  display: grid;
  gap: 2rem;
  margin: 1rem auto;
  max-width: 90%;
}
</style>
