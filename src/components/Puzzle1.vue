<script setup>
import { ref } from 'vue'

const emit = defineEmits(['next'])
const answer = ref("")
const error = ref(false)

const checkAnswer = () => {
  if (answer.value.toLowerCase().includes('thursday') || answer.value.includes('星期四')) {
    emit('next')
  } else {
    error.value = true
    setTimeout(() => error.value = false, 1000)
  }
}
</script>

<template>
  <div class="puzzle-container">
    <h2>System Locked. Authorization Required.</h2>
    <p class="clue">The day of madness. The day of craving.</p>
    <div class="input-group">
      <input 
        v-model="answer" 
        @keyup.enter="checkAnswer" 
        type="text" 
        placeholder="Enter Passcode" 
        :class="{ error: error }"
        autofocus
      />
      <button @click="checkAnswer">UNLOCK</button>
    </div>
    <p v-if="error" class="error-msg">ACCESS DENIED</p>
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
  text-shadow: 0 0 10px #0f0;
}

.clue {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  border-left: 2px solid #0f0;
  padding-left: 1rem;
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
  transition: transform 0.1s;
}

button:active {
  transform: scale(0.95);
}

.error-msg {
  color: red;
  margin-top: 1rem;
  font-weight: bold;
  text-shadow: 0 0 5px red;
}
</style>
