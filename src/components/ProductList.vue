<template>
  <div>
    <div
      class="row d-flex mb-3 align-items-center"
      v-for="(item, index) in products"
      :key="item.id"
      v-if="item.price <= Number(maximum)"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button class="btn btn-info" @click="$emit('add', item)">+</button>
      </div>
      <div class="col-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.title" />
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.title }}</h3>
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right"><price :value="item.price"></price></div>
      </div>
    </div>
  </div>
</template>

<script>
import price from "./price";

export default {
  name: "product-list",
  props: ["products", "maximum"],
  components: {
    price,
  },
};
</script>