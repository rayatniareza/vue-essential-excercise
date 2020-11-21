<template>
  <span
    >'{{
      this.prefix +
      Number(this.value * this.conversion).toFixed(this.percision)
    }}'</span
  >
</template>


<script>
export default {
  name: "price",
  props: {
    prefix: {
      type: String,
      default: "$",
    },
    value: Number,
    conversion: {
      type: Number,
      default: 1,
    },
    percision: {
      type: Number,
      default: 2,
    },
  },
};
</script>