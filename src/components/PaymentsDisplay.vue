<template>
  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Date</th>
      <th scope="col">Category</th>
      <th scope="col">Value</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item, idx) of items" :key="idx">
      <th scope="row">{{idx+1}}</th>
      <td>{{item.date}}</td>
      <td>{{item.category}}</td>
      <td>{{item.value}}</td>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'PaymentsDisplay',
  props: {
    items: {
      type: Array,
      default: [],
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
