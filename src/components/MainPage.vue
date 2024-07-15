<template>
  <div>
    <div class="button-container">
      <button @click="showProject = 1">1. ToDo List</button>
      <button @click="showProject = 2">2. Random Quote Generator</button>
      <button @click="showProject = 3">3. Calculator</button>
      <button @click="showProject = 4">4. Accordion</button>
      <button @click="showProject = 5">5. Form Validation</button>
      <button @click="showProject = 6">6. Password Generator</button>
    </div>
    <hr>
    <div v-if="showProject === 1"><Proj1Comp/></div>
    <div v-if="showProject === 2"><Proj2Comp/></div>
    <div v-if="showProject === 3"><Proj3Comp/></div>
    <div v-if="showProject === 4"><Proj4Comp/></div>
    <div v-if="showProject === 5"><Proj5Comp/></div>
    <div v-if="showProject === 6"><Proj6Comp/></div>
  </div>
</template>

<script setup>
import { ref, defineProps, watch } from 'vue';
import Proj1Comp from './1ToDoList';
import Proj2Comp from './2RandomQuote';
import Proj3Comp from './3Calculator';
import Proj4Comp from './4Accordion';
import Proj5Comp from './5FormValidation';
import Proj6Comp from './6PasswordGenerator';

const showProject = ref(0);
const props2 = defineProps(['resetValue'])
watch(() => props2.resetValue, () => {        // Reset showProject to 0 whenever resetValue changes
  showProject.value = 0;
});

</script>

<style scoped>
.button-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
button {
  display: block;
  width: 30rem;
  height: 1.5rem;
  margin: 1px 0;
}
</style>

