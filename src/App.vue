<template>
  <div class="container mt-2">
    <div class="form-label">
      <input class="form-control" v-model="operand1"/>
      <input class="form-control" v-model="operand2"/>
      = {{ result }}
    </div>
    <div class="keyboard">
      <button class="btn btn-secondary me-2" @click="result = Number(operand1) + Number(operand2)">+</button>
      <button class="btn btn-secondary me-2" @click="result = operand1 - operand2">-</button>
      <button class="btn btn-secondary me-2" @click="result = operand1 / operand2">/</button>
      <button class="btn btn-secondary me-2" @click="result = operand1 * operand2">*</button>
      <button class="btn btn-secondary me-2" @click="result = Math.pow(operand1, operand2)">x<sup>y</sup></button>
      <button class="btn btn-secondary me-2" @click="result = Math.floor(operand1 / operand2)">/(целое)</button>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      operand1: 0,
      operand2: 0,
      result: 0
    }
  },
  // components: {
  //   HelloWorld
  // }
}
</script>

<style lang="scss">
input{
  max-width: 200px;
}
</style>
