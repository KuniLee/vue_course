<template>
  <button @click="$emit('onClick')" type="button" class="btn"
  :class="{ 'btn-primary': !settings['bg-color']}"
      :style="{ background: settings['bg-color']}">
  {{ settings.text.toUpperCase() }}+</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    settings: {
      type: Object,
    }
  },
}
</script>

<style scoped>
</style>