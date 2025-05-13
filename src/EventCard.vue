<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpg'
import socksBlueImage from './assets/images/socks_blue.jpg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = true
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image : socksGreenImage},
  { id: 2235, color: 'blue',image : socksBlueImage},
])

const cart = ref(0)
const addToCart = () => {
      cart.value++
}

const UpdateImage = (variantImage) =>{
  image.value =variantImage
}
</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-bind:src="image">
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul class="bg-red-200 pl-4 mb-4">
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
          v-for="variant in variants"
          :key="variant.id"
          @mouseover="UpdateImage(variant.image)"
          class="color-circle"
          :style="{backgroundColor: variant.color}"
        >
          <!-- {{ variant.color }} -->
        </div>
        <button @click="addToCart" class="button">Add to Cart</button>
      </div>
    </div>
  </div>
</template>
