<template>
  <div>
    <div class="operands">
      <input v-model.number="operand1" type="number">
      <input v-model.number="operand2" type="number">
      <div class="result">{{ result }}</div>
    </div>

    <div class="buttons">
      <button @click="result = operand1 + operand2">+</button>
      <button @click="result = operand1 - operand2">-</button>
      <button @click="result = operand1 * operand2">*</button>
      <button @click="result = operand1 / operand2">/</button>
      <button @click="result = Math.floor(operand1 / operand2)">//</button>
      <button @click="result = operand1 ** operand2">x^y</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FirstCalc',
  data () {
    return {
      operand1: 0,
      operand2: 0,
      result: 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  button {
    width: 40%;
    font-size: 18px;
  }
</style>
