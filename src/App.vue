<template>
  <div>
    <img @click="resetProject" alt="Vue logo" src="./assets/logo.png" style="height: 3rem;">
    <MainPage :resetValue="resetValue"/>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MainPage from './components/MainPage';

const resetValue = ref(0);
const resetProject = () => {
  resetValue.value++;
  alert(`reset this from showProject: ${resetValue.value}`)
};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 5px;
}
</style>

