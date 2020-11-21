<template>
  <div id="app">
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle="toggleSliderStatus"
      @delete="deleteItem"
    />
    <price-slider :sliderStatus="sliderStatue" :maximum.sync="max" />
    <product-list :products="products" :maximum="max" @add="addItem" />
  </div>
</template>

<script>
import ProductList from "./components/ProductList";
import PriceSlider from "./components/PriceSlider";
import Navbar from "./components/Navbar";

export default {
  name: "App",
  components: {
    ProductList,
    PriceSlider,
    Navbar,
  },
  data: function () {
    return {
      max: 99,
      products: null,
      cart: [],
      sliderStatue: true,
    };
  },
  computed: {
    cartTotal: function () {
      let sum = 0;
      for (key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      for (key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    },
  },
  methods: {
    toggleSliderStatus: function () {
      this.sliderStatue = !this.sliderStatue;
    },
    deleteItem: function (index) {
      if (this.cart[index].qty > 1) {
        this.cart[index].qty--;
      } else {
        this.cart.splice(index, 1);
      }
    },
    addItem: function (product) {
      var index = this.cart.findIndex((item) => item.product.id === product.id);
      if (index !== -1) {
        this.cart[index].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
  },
  mounted: function () {
    fetch("https://fakestoreapi.com/products")
      .then((response) => response.json())
      .then((data) => (this.products = data));
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
