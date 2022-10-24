<template>
  <div class="container mt-2">
    <div class="form-label">
      <input class="form-control" v-model="operand1"/>
      <input class="form-control" v-model="operand2"/>
      = {{ result }}
    </div>
    <div class="keyboard">
      <button class="btn btn-secondary me-2" v-for="item of operands" @click="currentOperation=item">{{ item }}</button>
    </div>
    <div class="alert alert-danger my-2" v-show="error">Ошибка! {{ error }}</div>

    <ul class="list-group">
      <li class="list-group-item" v-for="(log, index) in logs" v-bind:key="index">{{ log }}</li>
    </ul>

  </div>

</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return {
      operands: ['+', '-', '/', '*', '**', '/целое'],
      currentOperation: "+",
      operand1: 0,
      operand2: 0,
      error: "",
      logs: {},
    }
  },
  computed: {
    result() {
      return this.calculate(this.currentOperation)
    }
  },
  methods: {
    calculate(operand) {
      this.error = ""
      switch (operand) {
        case "+":
          return this.sum()
        case "-":
          return this.minus()
        case "/":
          return this.divide()
        case "*":
          return this.mul()
        case "**":
          return this.pow()
        case "/int":
          return this.divInt()
      }
      this.$set(this.logs, Date.now(), `${this.operand1}${operand}${this.operand2}=${this.result}`)

    },
    sum() {
      return Number(this.operand1) + Number(this.operand2)
    },
    minus() {
      return this.operand1 - this.operand2
    },
    divide() {
      if (this.operand2 === 0) {
        this.error = "На ноль делить нельзя"
        return
      }
      return this.operand1 / this.operand2
    },
    mul() {
      return this.operand1 * this.operand2
    },
    pow() {
      return Math.pow(this.operand1, this.operand2)
    },
    divInt() {
      return Math.floor(this.operand1 / this.operand2)
    }
  }
  // components: {
  //   HelloWorld
  // }
}
</script>

<style lang="scss">
input {
  max-width: 200px;
}
</style>
