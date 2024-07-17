<template>
  <!-- Dynamic Class Binding - applies to this div and all its child -->
  <div :class="{ 'dark-theme': isDarkTheme}">     <!-- If isDarkTheme=true class is applied - <div class="dark-theme">  -->
    <div class="container">

      <div class="header-container">
        <h1>Search Wikipedia</h1>
        <span id="theme-toggler" @click="toggleTheme">{{ isDarkTheme ? 'Light': 'Dark' }}</span>   <!-- Toggle the text in span -->
      </div>

      <form @submit.prevent="submitSearch">
        <input type="text" id="search-input" v-model="searchQuery" placeholder="Enter Search Query">
        <button type="submit">Search</button>
      </form>

      <div id="search-result">
        <div v-if="isLoading" class="spinner">Loading...</div>    <!-- Show when isLoading=true -->
        <div v-if="searchResults.length">
          <div v-for="(result) in searchResults" :key="result.pageid" class="result-item">
            <a class="result-title"
                :href="`https://en.wikipedia.org/?curid=${result.pageid}`" target="_blank" rel="noopener">    <!-- Searched Title as link -->
                {{ result.title }}
            </a>
            <a class="result-link"
              :href="`https://en.wikipedia.org/?curid=${result.pageid}`"  target="_blank" rel="noopener">     <!-- The link as link -->
              {{ `https://en.wikipedia.org/?curid=${result.pageid}`}}
            </a>
            <p class="result-snippet" v-html="result.snippet"></p>                                            <!--result snippet (v-html - to render its actual content) -->
          </div>
        </div>
      </div>

    </div>
  </div>

</template>

<script setup>
import { ref } from 'vue'

const searchQuery = ref('')
const searchResults = ref([])
const isLoading = ref(false)
const error = ref(null)
const isDarkTheme = ref(false)

const toggleTheme = ()=> {                              //Toggler for theme <span>
  isDarkTheme.value = !isDarkTheme.value
}

const submitSearch = ()=> {                             //Main submit button function
  if (searchQuery.value.trim() !== '') {                //Check if <input> is not blank
    searchWikipedia(searchQuery.value)                  //Run searchWikipedia(<searchQuery) from <input>
  } else {
    searchResults.value = []
    error.value = 'Please enter a search query'
  }
}

const searchWikipedia = async (query)=> {
  const encodedQuery = encodeURIComponent(query) //SECURITY safely include input in a URL - returns a new string where certain characters are replaced representing the UTF-8 encoding.

  const endpoint = `https://en.wikipedia.org/w/api.php?action=query&list=search&prop=info&inprop=url&utf8=&format=json&origin=*&srlimit=10&srsearch=${encodedQuery}`
  try{
    isLoading.value = true                                //Run the loading spinner
    const response = await fetch(endpoint)                //Fetch request to endpoint
    const data =  await response.json()                   //Save to data parsed json object from response

    if (data.query && data.query.search) {                //Check if there are results
      searchResults.value = data.query.search
      error.value = null
    } else {
      searchResults.value = null
      error.value = 'No results found'
    }
  } catch(err) {                                            //Catch Error from Try-Catch
    console.error('Error fetching data: ', err)
    searchResults.value([])
    error.value = 'An error occured while fetching data'
  } finally {                                               //Finally - runs whether there is an error or none
    isLoading.value = false
  }
}

</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
}
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  text-align: left;
}
h1 {
  margin-bottom: 1rem;
}
#search-input {
  font-size: 1rem;
  padding: 0.5rem 1rem;
  margin-right: 1rem;
  border-radius: 0.25rem;
  flex-grow: 1;
}
#search-input:focus {
  border-color: #0074d9;
}
button[type='submit'] {
  font-size: 1.2rem;
  padding: 0.5rem 1rem;
  background-color: #0074d9;
  color: #fff;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
}
button[type='submit']:hover {
  background-color: #0063ad;
}
#search-results {
  margin-top: 2rem;
}
.result-item {
  margin-top: .8rem;
}
.result-title {
  font-size: 1.3rem;
  margin-bottom: 0;
}
.result-link {
  display: block;
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: #0074d9;
}
.result-link:hover {
  text-decoration: underline;
}
.result-snippet {
  margin-top: 0;
}
.spinner {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  height: 10rem;
}
.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
#theme-toggler {
  border: none;
  cursor: pointer;
  background: #e2e2e2;
  padding: 10px 20px;
  border-radius: 100px;
}
/* Dark theme */
.dark-theme {
  background-color: #282c34;
  color: #fff;
}
.dark-theme #search-input {
  background-color: #454545;
  color: #fff;
  border-color: #fff;
}
.dark-theme #search-input:focus {
  border-color: #0074d9;
}
.dark-theme button[type='submit'] {
  background-color: #0074d9;
}
.dark-theme .result-link,
.dark-theme .result-link:hover {
  color: #90caf9;
}
</style>