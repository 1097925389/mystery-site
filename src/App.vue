<script setup>
import { ref } from 'vue'
import Intro from './components/Intro.vue'
import Puzzle1 from './components/Puzzle1.vue'
import Puzzle2 from './components/Puzzle2.vue'
import Reveal from './components/Reveal.vue'

const currentStage = ref(0)

const nextStage = () => {
  currentStage.value++
}
</script>

<template>
  <div class="app-container">
    <Transition name="fade" mode="out-in">
      <Intro v-if="currentStage === 0" @next="nextStage" />
      <Puzzle1 v-else-if="currentStage === 1" @next="nextStage" />
      <Puzzle2 v-else-if="currentStage === 2" @next="nextStage" />
      <Reveal v-else-if="currentStage === 3" />
    </Transition>
  </div>
</template>

<style scoped>
.app-container {
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
