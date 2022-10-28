<template>
  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <li class="page-item" @click="prevPage">
        <a class="page-link" href="#" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li v-for="(page,idx) in  pageAmount" class="page-item" :class="{active:page===currentPage}"
          @click.prevent="changePage(idx)">
        <a class="page-link" href="#">{{ idx + 1 }}</a></li>
      <li class="page-item"  @click="nextPage">
        <a class="page-link" href="#" aria-label="Next">
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Pagination",
  computed: {
    pageAmount() {
      return Math.ceil(this.itemAmount / 10)
    }
  },
  data() {
    return {
      currentPage: Math.ceil(this.itemAmount / 10)
    }
  },
  props: {
    value: Number,
    itemAmount: {
      type: Number,
      default: 0,
    }
  },
  created() {
    this.$emit('input', this.currentPage)
  },
  updated() {
    this.$emit('input', this.currentPage)
  },
  methods: {
    changePage(page) {
      this.currentPage = page + 1
      this.$emit('input', this.currentPage)
    },
    prevPage() {
      if (this.currentPage > 1) this.currentPage--
      this.$emit('input', this.currentPage)
    },
    nextPage() {
      if (this.currentPage< this.pageAmount) this.currentPage++
      this.$emit('input', this.currentPage)
    }
  }
}
</script>

<style scoped>

</style>