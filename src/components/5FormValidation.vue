<template>
  <h2>5. Form Validation</h2>
  <h3 style="font-size: 1rem;">Takeways: v-if(), String trim/regex/length, form-submit.prevent , :disabled </h3>
  <div>
    <form @submit.prevent="submitForm" class="custom-form">
      <div class="form-group">
        <label for="name">Name: </label>
        <input v-model="formData.name" type="text" id="name">
        <span v-if="!isNameValid" class="error">Name is required</span>
      </div>
      <div class="form-group">
        <label for="email">Email: </label>
        <input v-model="formData.email" type="text" id="email">
        <span v-if="!isEmailValid" class="error">Enter a valid email</span>
      </div>
      <div class="form-group">
        <label for="password">Password: </label>
        <input v-model="formData.password" type="text" id="password">
        <span v-if="!isPasswordValid" class="error">Password must be at least 8 characters</span>
      </div>

      <button type="submit" :disabled="!isPasswordValid" class="submit-button">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
const formData = ref({
  name: '',
  email: '',
  password: ''
})

//VALIDATIONS
const isNameValid = computed(()=> formData.value.name.trim() !== '')                                  //Check Not Empty after trimming whitespace
const isEmailValid = computed(()=> /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email))           //See REGEX
const isPasswordValid = computed(()=> formData.value.password.length >= 8)                            //Character length
const isFormValid = computed(()=> isNameValid.value  && isEmailValid.value && isPasswordValid.value)  //For button enable if all is true

const submitForm = ()=> {
  if (isFormValid.value) {
    console.log('Form submitted: ', formData.value)
  } else {
    console.log('Invalid data')
  }
}
</script>

<style scoped>
.custom-form {
  max-width: 400px;
  margin: 0 auto;
}
.form-group {
  text-align: left;
  margin-bottom: 20px;
}
label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
}
input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.error {
  color: #e74c3c;
  font-size: 14px;
  margin-top: 5px;
}
.submit-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.submit-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}
</style>