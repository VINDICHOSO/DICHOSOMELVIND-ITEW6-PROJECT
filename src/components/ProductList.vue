<template>
    <div>
      <h1 class="product-title" style="display: flex; font-size: 70px; margin-top: 3%; justify-content: center; align-items: center;;">VIN'S MOTOR PARTS</h1>
      <div class="search-container">
        <h3 class="search-title">LIST OF MOTORCYCLE PARTS</h3>
        <input type="text" v-model="searchQuery" placeholder="Type here...">
      </div>
      <div class="product-container">
        <ul class="product-list">
          <li v-if="filteredProducts.length === 0" class="no-results">No matching products found.</li>
          <li v-for="product in filteredProducts" :key="product.id" class="product-item">
            <div class="product-info">
              <img :src="product.image" alt="Product Image" class="product-image">
              <div>
                <p class="product-name">{{ product.name }}</p>
                <p class="product-price">Php {{ product.price }}</p>
              </div>
            </div>
            <button @click="addToCart(product)" class="add-to-cart-btn">Add to Cart</button>
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchQuery: 'TMX',
        products: [
          { id: 1, name: 'TMXCarburator', price: 180, image: '/img/img10.png' },
          { id: 2, name: 'tmx125 Block 125cm', price: 2500, image: '/img/img13.png' },
          { id: 3, name: 'tmx155 Block 154cm', price: 4000, image: '/img/img13.png' },
          { id: 4, name: 'TMX155 Gas Tank', price: 3000, image: '/img/img14.png' },
          { id: 5, name: 'TMX155 Gas Tank', price: 145, image: '/img/img14.png' },
          { id: 6, name: 'TMX155 Gas Tank', price: 120, image: '/img/img14.png' },
          { id: 7, name: 'TMX155 Gas Tank', price: 160, image: '/img/img14.png' },
          { id: 8, name: 'TMX155 Gas Tank', price: 190, image: '/img/img14.png' },
          { id: 9, name: 'TMX155 Gas Tank', price: 170, image: '/img/img14.png' }
        ]
      };
    },
    computed: {
      filteredProducts() {
        if (!this.searchQuery.trim()) {
          return [];
        }
        const query = this.searchQuery.toLowerCase();
        return this.products.filter(product =>
          product.name.toLowerCase().includes(query)
        );
      }
    },
    methods: {
      addToCart(product) {
        this.$emit('add-to-cart', product);
      }
    }
  };
  </script>
  
  <style>
  
  .product-title {
   
    color: orangered;
    margin-bottom: 20px;
  }
  
  .search-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .search-title {
    font-size: 20px;
    color: #ff0;
    margin-bottom: 10px;
  }
  
  input[type="text"] {
    width: 500px;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  
  .input-container {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .product-container {
    background-color:  black;
    opacity: 80%;
    margin-top: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 20px;
    max-height: 400px; /* Limit the height of the container */
    overflow-y: auto; /* Enable vertical scroll */
  }
   /* Style the scrollbar */
   .product-container::-webkit-scrollbar {
    width: 6px;
    background-color: #000; /* Background color behind the scrollbar */
  }
  
  /* Track */
  .product-container::-webkit-scrollbar-track {
    background: #000; /* Color of the scrollbar track */
  }
  .product-container::-webkit-scrollbar-thumb {
    background: #ffc107; /* Color of the scrollbar handle */
    border-radius: 2px;
  }
  
  .product-list {
    list-style: none;
    padding: 0;
    display: grid;
    grid-template-columns: repeat(3, 1fr); 
    gap: 20px; 
  }
  
  .product-item {
    background-color: transparent;
    opacity: 120%;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0px 0px 10px rgba(255, 0, 0, 0.708);
    display: flex;
    flex-direction: column;
  }
  
  .product-info {
    display: flex;
    align-items: center;
  }
  
  .product-image {
    width: 80px;
    height: 80px;
    border-radius: 10px;
    border: 2px solid transparent;
    margin-right: 20px;
  }
  
  .product-name {
    color: #fff;
  }
  
  .product-price {
    color: #fff;
  }
  
  .add-to-cart-btn {
    background-color: #ff0;
    color: #000;
    border: none;
    padding: 8px 15px;
    font-size: 12px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s;
  }
  
  .add-to-cart-btn:hover {
    background-color: #ffc107;
    color: #000;
  }
  
  .no-results {
    color: #ff0;
    font-style: italic;
  }
  </style>
  