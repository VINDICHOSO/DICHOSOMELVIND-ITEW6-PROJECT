<template>
  <div class="main">
    <div class="app-container" style="background-image: url('/img/img11.jpg'); background-size: cover; height: 100vh; display: flex;">
    <ProductList @add-to-cart="addToCart"></ProductList>
    <ShoppingCart :cartItems="cartItems" @remove-from-cart="removeFromCart"></ShoppingCart>
  </div>
  </div>
  
</template>

<script>

import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  components: {
 
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      cartItems: []
    };
  },
  methods: {
    addToCart(product) {
      const existingItem = this.cartItems.find(item => item.id === product.id);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cartItems.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(item) {
      const index = this.cartItems.findIndex(cartItem => cartItem.id === item.id);
      if (index !== -1) {
        this.cartItems.splice(index, 1);
      }
    }
  }
};
</script>

<style scoped>
body{
  background: green;

}
.app-container {
  display: flex;
  justify-content: space-around;
  align-items: flex-start;
  padding: 10px;
  background-color: green;

 
}
</style>
