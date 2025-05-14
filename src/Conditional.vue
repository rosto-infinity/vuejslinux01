<script setup>
// cDéclaration d'une référence réactive pour gérer le stock
import { ref } from 'vue'
const inventory = ref(100) // Valeur initiale : 8 unités
</script>

<template>
  <!-- cAffichage conditionnel basé sur la quantité en stock -->
  <div class="stock-status">
    <!-- fCas 1 : Stock abondant (>10 unités) -->
    <p v-if="inventory > 10" class="in-stock">
      In Stock
    </p>

    <!-- dCas 2 : Stock limité (1-10 unités) -->
    <p v-else-if="inventory > 0" class="low-stock"> <!-- Optimisation : simplification de la condition -->
      Almost out of Stock ==> {{ inventory }} left <!-- Ajout du compteur -->
    </p>

    <!-- fCas 3 : Rupture de stock -->
    <p v-else class="out-of-stock">
      Out of Stock
    </p>
  </div>
</template>

<style scoped>
/* --Styles pour chaque état */
.stock-status p { padding: 0.5rem; border-radius: 4px; }
.in-stock { color: green; background-color: #f0fff0; }
.low-stock { color: orange; background-color: #fff8e6; }
.out-of-stock { color: red; background-color: #fff0f0; }
</style>
