<script setup>
 import {ref,} from 'vue'
 import stocksGreenImage from './assets/images/socks_blue.jpg'
import Other from './Other.vue'

 const product =ref('STOCKS prof')
 const description =ref('Lorem ipsum dolor  Lorem ipsum dolorLorem ipsum dolorLorem ipsum dolorLorem ipsum dolorLorem ipsum dolorLorem ipsum dolor')
const image =ref(stocksGreenImage)

const inStock =ref(true)
const inventory =ref(8)

</script>
<template>
  <div class="nav-bar"></div>
<div class="product-display">
  <div class="product-container">
    <div class="product-image">
      <!-- image goes herennh -->
       <img :src="image" alt="stok green">  
    </div>
    <div class="product-info">
      <h1>{{ product }}</h1>
      <!-- <p> {{ description }}</p> -->
      <hr class="mb-4">
      <p v-show="inStock">In Stock</p>
      <p v-if="inventory > 10">In Stock 2</p>
      <p v-else-if="inventory <10 && inventory >0">Almost of Stock ==></p>
      <p v-else>Out of Stock</p>
      <!-- <p v-else>Out of Stock</p> -->
    </div>
  </div>
</div>
<Other/>
</template>
<style scoped>
</style>
