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
import axios from 'axios'       //Axios Import
const joke = ref(null)

const fetchJoke = async()=> {                                               //Async -> Function
  try {
    const response = await axios.get('https://icanhazdadjoke.com', {        //Await -> Axios.get
      headers: {Accept: 'application/json'}                                 //Tells the server that the client expects a JSON response.
    })
    joke.value = response.data.joke
  } catch(error) {                                                          //Catch Error
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
  border: none;
  cursor: pointer;
}
.dad-joke {
  padding: 15px;
  margin-top: 20px;
}
</style>