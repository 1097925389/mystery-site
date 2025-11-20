<script setup>
import { ref } from 'vue'

const emit = defineEmits(['next'])
const answer = ref("")
const error = ref(false)

const checkAnswer = () => {
  if (answer.value === '50') {
    emit('next')
  } else {
    error.value = true
    setTimeout(() => error.value = false, 1000)
  }
}
</script>

<template>
  <div class="puzzle-container">
    <h2>Level 2 Security Clearance</h2>
    <p class="clue">What is the price of sanity?</p>
    <div class="code-block">
      V = ?
    </div>
    <div class="input-group">
      <input 
        v-model="answer" 
        @keyup.enter="checkAnswer" 
        type="text" 
        placeholder="Enter Value" 
        :class="{ error: error }"
        autofocus
      />
      <button @click="checkAnswer">DECRYPT</button>
    </div>
    <p v-if="error" class="error-msg">INVALID VALUE</p>
  </div>
</template>

<style scoped>
.puzzle-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #050505;
  color: #0f0;
  font-family: 'Courier New', Courier, monospace;
}

h2 {
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 2rem;
  color: #0f0;
}

.clue {
  font-size: 1.2rem;
  margin-bottom: 1rem;
}

.code-block {
  background: #001100;
  padding: 1rem 2rem;
  border: 1px dashed #0f0;
  margin-bottom: 2rem;
  font-size: 1.5rem;
  font-weight: bold;
}

.input-group {
  display: flex;
  gap: 1rem;
}

input {
  background: transparent;
  border: 1px solid #0f0;
  color: #0f0;
  padding: 0.5rem 1rem;
  font-family: inherit;
  font-size: 1.2rem;
  outline: none;
  transition: all 0.3s;
}

input:focus {
  box-shadow: 0 0 15px #0f0;
}

input.error {
  border-color: red;
  color: red;
  box-shadow: 0 0 15px red;
}

button {
  background: #0f0;
  color: black;
  border: none;
  padding: 0.5rem 1.5rem;
  font-family: inherit;
  font-weight: bold;
  cursor: pointer;
}

.error-msg {
  color: red;
  margin-top: 1rem;
  font-weight: bold;
  text-shadow: 0 0 5px red;
}
</style>
