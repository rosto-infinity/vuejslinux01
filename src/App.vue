<script setup>
 import {ref,} from 'vue'
 import stocksGreenImage from './assets/images/socks_blue.jpg'
import Other from './Other.vue'
import Conditional from './Conditional.vue'
import List from './List.vue'

 const product =ref('STOCKS prof')
 const description =ref('Lorem ipsum dolor  Lorem ipsum dolorLorem ipsum dolorLorem ipsum dolorLorem ipsum dolorLorem ipsum dolorLorem ipsum dolor')
const image =ref(stocksGreenImage)

const inStock =ref(true)


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
      <p> {{ description }}</p>
      <p v-if="inStock">In Stock</p> 
     <p v-else>Out of Stock</p>
      <hr class="mb-4">
     <List/>
      <Conditional/>
      <Other/>
    </div>
  </div>
</div>
</template>
<style scoped>
</style>
