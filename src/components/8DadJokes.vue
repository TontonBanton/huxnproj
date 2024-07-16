<template>
  <h2>8. Dad Jokes</h2>
  <h3 style="font-size: 1rem;">Takeways: Axios, async-await(), try-catch{}</h3>
  <div class="dad-jokes-container">
    <button @click="fetchJoke" class="get-joke-button">Get Dad Joke</button>
    <div class="dad-joke">{{ joke }}</div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const joke = ref(null)

const fetchJoke = async()=> {
  try {
    const response = await axios.get('https://icanhazdadjoke.com', {
      headers: {Accept: 'application/json'}
    })
    joke.value = response.data.joke
  } catch(error) {
    console.error('Error fetching data:', error)
  }
}

</script>

<style scoped>
.dad-jokes-container {
  max-width: 600px;
  margin: 50px auto;
}
.get-joke-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.dad-joke {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 15px;
  margin-top: 20px;
  background-color: #f9f9f9;
  color: #333;
}
</style>