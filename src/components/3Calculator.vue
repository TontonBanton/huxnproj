<template>
  <h2>Calculator</h2>
  <h3 style="font-size: 1rem;">Takeways: computed(), :class (Dynamic Class binding), eval (Evaluate expression as string - Not recommended)</h3>
  <div class="calculator">
    <input v-model="display" :class="displayClass" readonly>
    <div class="buttons">
      <button @click="appendToDisplay('7')">7</button>
      <button @click="appendToDisplay('8')">8</button>
      <button @click="appendToDisplay('9')">9</button>
      <button @click="appendToDisplay('/')">/</button>

      <button @click="appendToDisplay('4')">4</button>
      <button @click="appendToDisplay('5')">5</button>
      <button @click="appendToDisplay('6')">6</button>
      <button @click="appendToDisplay('*')">*</button>

      <button @click="appendToDisplay('1')">1</button>
      <button @click="appendToDisplay('2')">2</button>
      <button @click="appendToDisplay('3')">3</button>
      <button @click="appendToDisplay('-')">-</button>

      <button @click="appendToDisplay('0')">0</button>
      <button @click="appendToDisplay('.')">.</button>
      <button @click="calculate">=</button>
      <button @click="appendToDisplay('+')">+</button>
    </div>
    <button @click="clearDisplay" class="clear-button">Clear</button>

  </div>

</template>

<script setup>
import { ref, computed } from 'vue'
const display = ref(0)

//For Individual Button
const appendToDisplay = (value)=> {
  if (display.value === '0' && value !== '.' ) {        //Check if it is 0 or decimal
    display.value = value
  } else {
    display.value += value
  }
}

//For Equal (=) button only
const calculate = ()=> {
  try {
    display.value = eval(display.value).toString()      //Evaluate string as expression ex. '1 + 1'
  } catch {
    display.value = 'Error'
  }
}

//Computed Property for dynamic class binding (if length is too long)
const displayClass = computed(()=> {
  return display.value.length > 12 ? 'small-text' : ''  //change fontsize if display is 12+
})

//For Clear button only
const clearDisplay = ()=> {
  display.value = '0'
}

</script>

<style scoped>
input {
  padding: 10px 20px;
  margin-bottom: 20px;
}

.calculator {
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.display {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 18px;
  text-align: right;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  width: 100%;
  padding: 10px;
  font-size: 18px;
}

.clear-button {
  width: 100%;
  margin-top: 10px;
}

.small-text {
  font-size: 14px;
}
</style>