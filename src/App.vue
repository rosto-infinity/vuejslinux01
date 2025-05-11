<script setup>
 import {ref,} from 'vue'
 import stocksGreenImage from './assets/images/socks_green.jpg'

 const product =ref('STOCKS prof')
 const description =ref('Lorem ipsum dolor ')
const image =ref(stocksGreenImage)

</script>
<template>
  <div class="nav-bar"></div>
<div class="product-display">
  <div class="product-container">
    <div class="product-image">
      <!-- image goes here -->
       <img v-bind:src="image" alt="stok green">
    </div>
    <div class="product-info">
      <h1>{{ product }}</h1>
      <p> {{ description }}</p>
    </div>
  </div>
</div>
</template>
<style scoped>
</style>
