<template>
  <button
    class="btn"
    :class="color"
    @click="$emit('action')"
  >
  <slot/>
  </button>
</template>

<script>
export default {
  emits: ['action'],
  props: {
    color: {
      type: String,
      default: ''
    }
    // указываем slot и отказываемся от передачи параметров
    // text: {
    //   type: String,
    //   required: true
    // }
  },
  validator (value) {
    return ['', 'primary', 'danger'].includes(value)
  }
}
</script>

<style scoped>

</style>
