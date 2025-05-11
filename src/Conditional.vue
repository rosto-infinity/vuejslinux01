<script setup>
import {ref} from 'vue'
const inventory =ref(8)
</script>

<template>
      <p v-if="inventory > 10">In Stock 2</p>
      <p v-else-if="inventory <10 && inventory >0">Almost of Stock ==></p>
      <p v-else>Out of Stock</p>
</template>
