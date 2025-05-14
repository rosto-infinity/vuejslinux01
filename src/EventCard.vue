<script setup>
// Importation des fonctionnalités nécessaires de Vue et des images
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpg'
import socksBlueImage from './assets/images/socks_blue.jpg'

// Déclaration des variables réactives
const product = ref('Socks') // Nom du produit
const image = ref(socksGreenImage) // Image par défaut du produit
const inStock = true // Indique si le produit est en stock ou non

// Liste des détails du produit
const details = ref(['50% cotton', '30% wool', '20% polyester'])

// Variantes du produit avec leurs couleurs et images associées
const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage },
])

// Gestion du panier
const cart = ref(0) // Nombre d'articles dans le panier
const addToCart = () => {
  cart.value++ // Incrémente le panier lorsqu'un produit est ajouté
}

// Fonction pour mettre à jour l'image du produit en fonction de la variante sélectionnée
const UpdateImage = (variantImage) => {
  image.value = variantImage
}
</script>
  
<template>
  <!-- Barre de navigation -->
  <div class="nav-bar"></div>

  <!-- Affichage du panier -->
  <div class="cart">Cart({{ cart }})</div>

  <!-- Affichage principal du produit -->
  <div class="product-display">
    <div class="product-container">
      <!-- Section de l'image du produit -->
      <div class="product-image">    
        <img v-bind:src="image"> <!-- Image dynamique basée sur la variante sélectionnée -->
      </div>

      <!-- Informations sur le produit -->
      <div class="product-info">
        <h1>{{ product }}</h1> <!-- Nom du produit -->
        <p v-if="inStock">In Stock</p> <!-- Message si le produit est en stock -->
        <p v-else>Out of Stock</p> <!-- Message si le produit est en rupture de stock -->

        <!-- Liste des détails du produit -->
        <ul class="bg-red-200 pl-4 mb-4">
          <li v-for="detail in details">{{ detail }}</li>
        </ul>

        <!-- Variantes du produit (couleurs) -->
        <!-- l'image au survol  -->
        <!-- Style dynamique pour la couleur -->
        <div
          v-for="variant in variants"
          :key="variant.id"
          @mouseover="UpdateImage(variant.image)" 
          class="color-circle"
          :style="{ backgroundColor: variant.color }" 
        >
          <!-- {{ variant.color }} -->
        </div>

        <!-- Bouton pour ajouter au panier -->
        <button @click="addToCart" class="button">Add to Cart</button>
      </div>
    </div>
  </div>
</template>
