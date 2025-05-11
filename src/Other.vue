<script setup>
import stocksProductsImages from './assets/images/socks_green.jpg'
const props = defineProps({
  product: {
    type: Object,
    default: () => ({ image: stocksProductsImages, name: "Produit" }),
  },
});
</script>
<template>
  <img :src="product.image" :alt="`Image de ${product.name}`" />
</template>
