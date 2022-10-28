<template>
  <form @submit.prevent="addNew">
    <input required v-model="data.category" class="form-control my-2" type="text" placeholder="Payment description">
    <input required v-model="data.value" class="form-control my-2" type="number" placeholder="Payment amount">
    <input required v-model="data.date" class="form-control my-2" type="date" placeholder="Payment date">
    <Button type="submit"  :settings="{text: 'add'}"></Button>
  </form>
</template>

<script>
import Button from "@/components/Button";
export default {
  name: "NewCost",
  data(){
    return{
      data:{
        category:'',
        value:'',
        date:'',
      }
    }
  },
  methods:{
    addNew(){
      const newPay = {...this.data}
      newPay.date = newPay.date.split("-").reverse().join('.')
      this.data = {
        category:'',
        value:'',
        date:'',
      }
      this.$emit("onAdd", newPay)
    }
  },
  components: {Button}
}
</script>

<style scoped>

</style>