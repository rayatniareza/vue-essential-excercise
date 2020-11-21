<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button class="btn btn-sm btn-outline-success" @click="$emit('toggle')">
        <i class="fas fa-dollar-sign"></i>
        <font-awesome-icon icon="dollar-sign" />
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="cartDropdown"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <i class="fas fa-shopping-cart mx-2"></i>
          {{ cartTotal | currency }}
        </button>
        <div
          class="dropdown-menu dropdown-menu-right"
          aria-labelledby="cartDropdown"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span
                class="badge badge-pill badge-warning align-text-top mr-1"
                >{{ item.qty }}</span
              >
              {{ item.product.title }}
              <b><price :value="item.product.price * item.qty"></price></b>
              <a
                href="#"
                @click.stop="$emit('delete', index)"
                class="badge badge-danger text-white"
                >-</a
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>


<script>
import price from "./price";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "navbar",
  props: ["cart", "cartQty", "cartTotal"],
  components: {
    price,
    FontAwesomeIcon,
  },
  filters: {
    currency: function (value) {
      return "$" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>