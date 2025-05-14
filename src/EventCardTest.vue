<script setup>
// -Importation des fonctionnalités nécessaires de Vue et des images
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpg'
import socksBlueImage from './assets/images/socks_blue.jpg'

// -Déclaration des variables réactives
const image = ref(socksBlueImage) // Image par défaut du produit

// -Variantes du produit avec leurs couleurs et images associées
const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage },
])

// -Fonction pour mettre à jour l'image du produit en fonction de la variante sélectionnée
const UpdateImage = (variantImage) => {
  image.value = variantImage
}
</script>
  
<template>

    <!-- Affichage principal du produit -->
    <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img :src="image"> <!-- Image dynamique basée sur la variante sélectionnée -->
      </div>
        <!-- -Variantes du produit (couleurs) -->
        <!-- -l'image au survol  -->
        <!-- -Style dynamique pour la couleur -->
        <div
          v-for="variant in variants"
          :key="variant.id"
          @mouseover="UpdateImage(variant.image)" 
          class="color-circle"
          :style="{ backgroundColor: variant.color }" 
        >
          <!-- {{ -variant.color }} -->
        </div>
     </div>
  </div>
        

</template>
