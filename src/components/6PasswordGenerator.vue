<template>
  <h2>6. Password Generator</h2>
  <h3 style="font-size: 1rem;">Takeways: v-model, for-Loop, Math floor/random, length, concatenate =+</h3>
  <div class="password-generator-container">
    <label>Password Length</label>
    <input type="number" v-model="passwordLength" min="4" max="32" style="width: 90%"/><br/>
    <label>Include Uppercase</label>
    <input type="checkbox" v-model="includeUppercase"/><br/>
    <label>Include Numbers</label>
    <input type="checkbox" v-model="includeNumbers"/><br/>
    <label>Include Symbols</label>
    <input type="checkbox" v-model="includeSymbols"/><br/>

    <button @click="generatePassword" class="generate-button">Generate password</button>
  </div>
  <div v-if="generatePassword" class="generated-password">
    <strong>Your Password:</strong> {{ generatedPassword }}
  </div>
</template>

<script setup>
import { ref } from 'vue'

const passwordLength = ref(12)          //bind w/ input bux
const includeUppercase = ref(true)      //bindings w/ checkbox status
const includeNumbers = ref (true)       //bindings w/ checkbox status
const includeSymbols = ref (true)       //bindings w/ checkbox status
const generatedPassword = ref('')

//Button Click
const generatePassword = ()=> {
  const lowercaseChars = "abcdefghijklmnopqrstuvwxyz";                                  //provide lowercase (default)
  const uppercaseChars = includeUppercase.value ? "ABCDEFGHIJKLMNOPQRSTUVWXYZ" : "";    //provide uppercase characters if checkbox is true else ''
  const numberChars = includeNumbers.value ? "0123456789" : "";                         //provide number if number checkbox is true else ''
  const symbolChars = includeSymbols.value ? "!@#$%^&*()_+[]{}|;:,.<>?/~`" : "";        //provide symbols if symbols checkbox is true else ''
  const allChars = lowercaseChars + uppercaseChars + numberChars + symbolChars;         //concatenate all characters

  let password = ''
  for (let i =0; i < passwordLength.value; i++) {                     //Loop number of length from input passwordLength bind
    const randomIndex = Math.floor(Math.random() * allChars.length)   //Get random index
    password += allChars[randomIndex]                                 //Get random index character concatenate to password loop again
  }
  generatedPassword.value = password                                  //Save all charaacters
}

</script>

<style scoped>
.password-generator-container {
  max-width: 400px;
  margin: 15px auto;
  text-align: left;
}
input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}
.generate-button {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  background-color: #3498db;
  border: none;
}
.generate-button:hover {
  background-color: #2980b9;
}
.generated-password {
  margin-top: 5px;
}
</style>