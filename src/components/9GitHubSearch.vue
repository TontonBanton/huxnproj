<template>
  <h2>GitHub User Search</h2>
  <h3 style="font-size: 1rem;">Takeways: fetch(api), async-await(), try-catch{}, response.json</h3>
  <div class="github-profile-viewer">
    <div class="input-container">
      <input v-model="userName" placeholder="Enter GitHub username" @input="getUserProfile">
    </div>
    <div v-if="user-profile" class="user-profile">
        <img :src="userProfile.avatar_url">
        <div class="user-details">
          <p><strong>Name:</strong> {{ userProfile.login }}</p>
          <p><strong>Location:</strong> {{ userProfile.location }}</p>
          <p><strong>Followers:</strong> {{ userProfile.followers }}</p>
          <p><strong>Following:</strong> {{ userProfile.following }}</p>
          <p><strong>Public Repos:</strong> {{ userProfile.public_repos }}</p>
        </div>
    </div>

    <div v-if="error" class="error-message">
      <p>{{ error }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const userName = ref('')
const userProfile = ref(null)
const error = ref(null)

const getUserProfile = async()=> {                                                  //Async->function
  try {
    const response = await fetch(`https://api.github.com/users/${userName.value}`)    //Await fetch() from GitHub API list of users in JSON format
    const data = await response.json()                                                //Save parsed response body text as JSON -> data

    if (response.ok) {                //Check if response ok
      userProfile.value = data
      error.value = null
    } else {                          //Response is not ok
      userProfile.value = null
      error.value = data.message
    }

  } catch(err) {                                                                    //Catch Error from Try-Catch
    console.error('Error fetching data: ', err)
    error.value = 'An error occured while fetching data'
  }
}
</script>

<style scoped>
.github-profile-viewer {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.input-container {
  margin-bottom: 20px;
}
input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
}
.user-profile {
  margin-top: 20px;
}
h2 {
  font-size: 20px;
  margin-bottom: 10px;
  color: #333;
}
img {
  width: 150px;
  border-radius: 50%;
  margin-bottom: 20px;
}
.user-details {
  text-align: left;
}
p {
  font-size: 16px;
  margin-bottom: 10px;
}
.error-message {
  color: #e74c3c;
  margin-top: 20px;
}
</style>
