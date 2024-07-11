<template>
  <div class="button-container">
    <button @click="showProject = 1">1. ToDo List</button>
    <button @click="showProject = 2">2. Random Quote Generator</button>
  </div>

  <div v-if="showProject === 1">
    <Proj1Comp/>
  </div>
  <div v-if="showProject === 2">
    <Proj2Comp/>
  </div>

</template>

<script setup>
import { ref } from 'vue'
import Proj1Comp from './1ToDoList'
import Proj2Comp from './2RandomQuote'


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
  width: 50rem; /* Set button width */
  height: 3rem; /* Set button height */
  margin: 5px 0; /* Optional: Add some margin between the buttons */
}
</style>
