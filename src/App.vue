<template>
  <div class="container">
    <h1>My personal costs</h1>
    <Button v-if="!openedAdd" @onClick="openedAdd=!openedAdd" :settings='{text:"ADD NEW COST"}'
    ></Button>
    <NewCost v-if="openedAdd" @onAdd="add"></NewCost>
    <PaymentsDisplay class="w-50" :items="paymentsList"/>
  </div>
</template>

<script>
import PaymentsDisplay from "@/components/PaymentsDisplay";
import Button from "@/components/Button";
import NewCost from "@/components/NewPayment";

export default {
  name: 'App',
  data() {
    return {
      openedAdd: false,
      paymentsList: []
    }
  },
  methods: {
    add(el) {
      this.openedAdd = false
      this.paymentsList.push(el)
    },
    fetchData() {
      function generateItem(){
        return  {
          date: '28.03.2020',
          category: 'Food',
          value: Math.floor(Math.random()*1000),
        }
      }
      const list = []
      for (let i = 0; i < 30; i++) {
        list.push(generateItem())
      }
      return list
    },
  },
  created() {
    this.paymentsList = this.fetchData()
  },
  components: {
    NewCost,
    Button,
    PaymentsDisplay
  }
}
</script>

<style lang="scss">
input {
  max-width: 200px;
}
</style>
