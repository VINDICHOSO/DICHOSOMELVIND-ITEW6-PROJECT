<template>
    <div class="cart-container">
        <h2 class="cart-title" style="color: red; font-size: 30px;"><img src="/img/img12.png" style="width: 50px; height: 50px;">    CART LIST</h2>
      <ul>
        <li v-for="item in cartItems" :key="item.id" class="cart-item">
          <div class="cart-item-details">
            <img :src="item.image" alt="Product Image" class="cart-item-image">
            <div class="item-details">
              <h3>{{ item.name }}</h3>
              <p class="item-price">Php {{ item.price }} x {{ item.quantity }}</p>
              <div class="quantity-controls">
                <button @click="updateQuantity(item, 'decrease')" class="quantity-btn">-</button>
                <button @click="updateQuantity(item, 'increase')" class="quantity-btn">+</button>
              </div>
              <br>
              <button @click="removeFromCart(item)" class="remove-btn">Remove</button>
            </div>
          </div>
        </li>
      </ul>
      <div v-if="cartItems.length === 0" class="empty-cart">Your cart is empty.</div>
      <div v-else class="total-price">Total Price: Php {{ totalPrice }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['cartItems'],
    computed: {
      totalPrice() {
        return this.cartItems.reduce((total, item) => total + (item.price * item.quantity), 0);
      }
    },
    methods: {
      updateQuantity(item, action) {
        if (action === 'increase') {
          item.quantity++;
        } else if (action === 'decrease' && item.quantity > 1) {
          item.quantity--;
        }
      },
      removeFromCart(item) {
        this.$emit('remove-from-cart', item);
      }
    }
  };
  </script>
  
  <style scoped>
  .cart-container {
    width: 400px;
    background-color: #000;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0px 0px 20px rgba(255, 255, 0, 0.3);
    color: #fff;
    max-height: 650px; 
    overflow-y: auto; 
  }
  
  
  .cart-container::-webkit-scrollbar {
    width: 6px;
    background-color: #000; 
  }
  
  
  .cart-container::-webkit-scrollbar-track {
    background: #000; 
  }
  
  
  .cart-container::-webkit-scrollbar-thumb {
    background: #ffc107; 
    border-radius: 2px;
  }
  
  .cart-title {
    font-size: 24px;
    margin-bottom: 20px;
    color: #ff0;
  }
  
  .cart-item {
    margin-bottom: 20px;
  }
  
  .cart-item-details {
    display: flex;
    align-items: center;
  }
  
  .cart-item-image {
    width: 80px;
    height: 80px;
    margin-right: 20px;
    border-radius: 10px;
    border: 2px solid #ff0;
  }
  
  .item-details {
    flex: 1;
  }
  
  .item-price {
    margin: 5px 0;
    color: #ff0;
  }
  
  .remove-btn {
    background-color: #ff0;
    color: #000;
    border: none;
    padding: 8px 15px;
    font-size: 14px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s;
  }
  
  .remove-btn:hover {
    background-color: #ffc107;
    color: #000;
  }
  
  .total-price {
    font-size: 18px;
  }
  
  .quantity-controls {
    display: flex;
  }
  
  .quantity-btn {
    background-color: #ff0;
    color: #000;
    border: none;
    padding: 5px 10px;
    font-size: 14px;
    cursor: pointer;
    border-radius: 5px;
    margin-right: 5px;
    transition: background-color 0.3s;
  }
  
  .quantity-btn:hover {
    background-color: #ffc107;
    color: #000;
  }
  </style>