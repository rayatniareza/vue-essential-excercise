<template>
  <div v-if="sliderStatus">
    <div class="align-items-center" :class="sliderState">
      <label class="font-weight-bold mr-2" for="formMax">max</label>
      <input
        type="text"
        id="formMax"
        class="form-control mx-2"
        style="width: 60px"
        v-model="maxAmount"
        @change="$emit('update: ', maxAmount)"
      />
      <input
        type="range"
        class="custom-range"
        min="0"
        max="200"
        v-model="maxAmount"
        @change="$emit('update:maximum', maxAmount)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: 99,
    };
  },
  props: ["sliderStatus"],
  methods: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>