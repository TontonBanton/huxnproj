<template>
  <div class="button-container">
    <button @click="showProject = 1">1. ToDo List</button>
    <button @click="showProject = 2">2. Random Quote Generator</button>
    <button @click="showProject = 3">3. Calculator</button>
    <button @click="showProject = 4">4. Accordion</button>
  </div>
  <hr>

  <div v-if="showProject === 1"><Proj1Comp/></div>
  <div v-if="showProject === 2"><Proj2Comp/></div>
  <div v-if="showProject === 3"><Proj3Comp/></div>
  <div v-if="showProject === 4"><Proj4Comp/></div>

</template>

<script setup>
import { ref } from 'vue'
import Proj1Comp from './1ToDoList'
import Proj2Comp from './2RandomQuote'
import Proj3Comp from './3Calculator'
import Proj4Comp from './4Accordion'

const showProject = ref(0) //default value
</script>

<style scoped>
.button-container {
  display: flex;
  flex-direction: column;
  justify-content: center; /* Center vertically */
  align-items: center; /* Center horizontally */
}
button {
  display: block;
  width: 30rem; /* Set button width */
  height: 1.5rem; /* Set button height */
  margin: 1px 0; /* Optional: Add some margin between the buttons */
}
</style>
