<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['next'])
const text = "Wake up... The truth is hidden..."
const displayedText = ref("")
const showButton = ref(false)

onMounted(() => {
  let i = 0
  const interval = setInterval(() => {
    displayedText.value += text[i]
    i++
    if (i === text.length) {
      clearInterval(interval)
      showButton.value = true
    }
  }, 100)
})
</script>

<template>
  <div class="intro-container" @click="$emit('next')">
    <div class="terminal-text">{{ displayedText }}<span class="cursor">_</span></div>
    <div v-if="showButton" class="hint">[Click anywhere to initialize]</div>
  </div>
</template>

<style scoped>
.intro-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: black;
  color: #0f0;
  font-family: 'Courier New', Courier, monospace;
  cursor: pointer;
}

.terminal-text {
  font-size: 2rem;
  text-shadow: 0 0 5px #0f0;
}

.cursor {
  animation: blink 1s infinite;
}

.hint {
  margin-top: 2rem;
  opacity: 0.7;
  font-size: 0.8rem;
  animation: fade 2s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

@keyframes fade {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 1; }
}
</style>
