<template>
  <main>
    <header>
      <h1>Vue Ecommerce</h1>
      <span>Items on cart: {{ cart.length }}</span>
    </header>
    <product-display :premium="true" @add-to-cart="updateCart" />
  </main>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay";
export default {
  name: "App",
  components: {
    ProductDisplay,
  },
  data() {
    return {
      cart: [],
      premium: true,
    };
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 22px 16px;
}
header > h1 {
  font-size: 14px;
}
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.product__gallery,
.product__info {
  width: 50%;
}
.product__container {
  display: flex;
  max-width: 1200px;
  margin: 0 auto;
  margin-top: 40px;
  text-align: left;
}
.product__image {
  max-width: 100%;
}
</style>
