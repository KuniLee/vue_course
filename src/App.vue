<template>
  <div class="container mt-2 d-flex align-items-center flex-column">
    <div class="form-label">
      <input type="number" v-for="op of 2" class="form-control mb-2" @click="chooseOperand(op)" v-model="operand[op]"/>
      = {{ result }}
    </div>
    <div class="keyboard">
      <button class="btn btn-secondary me-2" :class="{ active: currentOperation===item }" v-for="item of operations"
          @click="currentOperation=item">{{ item }}
      </button>
    </div>
    <div class="alert alert-danger my-2" v-show="error">Ошибка! {{ error }}</div>
    <div class="my-2 d-flex align-items-center flex-column">
      <div><input type="checkbox" id="checkbox" v-model="vKeyBoard">
        <label class="ms-2" for="checkbox">Экранная клавиатура</label></div>
      <div v-if="vKeyBoard" class="">
        <div>Выбранный операнд: {{ chosenOperand }}</div>
        <button class="btn btn-outline-dark me-2" v-for="item of 9"
            @click="operand[chosenOperand]+=item.toString()">{{ item }}
        </button>
        <button class="btn btn-outline-dark me-2"
            @click="operand[chosenOperand]=operand[chosenOperand].toString().slice(0,-1)">
          &#8592;
        </button>
      </div>
    </div>

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
      chosenOperand: 1,
      vKeyBoard: false,
      operations: ['+', '-', '/', '*', '**', '/целое'],
      currentOperation: "+",
      operand: {
        1: 0,
        2: 0
      },
      error: "",
      logs: {},
    }
  },
  computed: {
    result() {
      const result  = this.calculate(this.currentOperation)
      return isNaN(result)? "" : result
    }
  },
  methods: {
    enter() {

    },
    chooseOperand(num) {
      this.chosenOperand = num
    },
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
        case "/целое":
          return this.divInt()
      }
      this.$set(this.logs, Date.now(), `${this.operand[1]}${operand}${this.operand[2]}=${this.result}`)

    },
    sum() {
      return Number(this.operand[1]) + Number(this.operand[2])
    },
    minus() {
      return this.operand[1] - this.operand[2]
    },
    divide() {
      if (this.operand[2] === 0) {
        this.error = "На ноль делить нельзя!"
        return
      }
      return this.operand[1] / this.operand[2]
    },
    mul() {
      return this.operand[1] * this.operand[2]
    },
    pow() {
      return Math.pow(this.operand[1], this.operand[2])
    },
    divInt() {
      if (this.operand[2] === 0) {
        this.error = "На ноль делить нельзя!"
        return
      }
      return Math.floor(this.operand[1] / this.operand[2])
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
