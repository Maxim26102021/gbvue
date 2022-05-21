<template>
  <button :disabled='show' @click="$emit('custom-event', operation)" class='btn'>{{ operation }}</button>
</template>

<script>
export default {
  props: {
    operation: {
      type: String,
      default: 'Start'
    },
    show: {
      type: Boolean,
      default: true,
    }
  },
  name: 'Buttons',

}

</script>

<style scoped>
  .btn {
    width: 50px;
    height: 20px;
    text-align: center;
  }
</style>