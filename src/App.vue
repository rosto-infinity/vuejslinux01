<script setup>
 import {ref,} from 'vue'
 const product =ref('STOCKS prof')
 const description =ref('Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi veniam hic quia eius debitis perspiciatis voluptas quasi nesciunt sed tenetur? Perspiciatis fuga alias sequi quae fugit similique nulla illo laborum?')
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-info text-center pt-20">
        <h1 class="text-8xl ">{{ product }}</h1>
        <p> {{ description }}</p>
        
      </div>
    </div>
  </div>
</template>
<style scoped>
</style>
