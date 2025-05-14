<script setup>
// -Importation de la fonction ref de Vue pour créer des données réactives
import { ref } from 'vue';

// -Liste des détails du produit
const details = ref([
  '50% aaaa', // Composition du produit
  '50% bbb',  // Composition du produit
  '80% cccc', // Composition du produit
  '90% ddd',  // Composition du produit
])

// -Variantes du produit avec leurs couleurs
const variants = ref([
  { id: 784, color: 'green' }, // -Variante avec couleur verte
  { id: 785, color: 'blue' },  // -Variante avec couleur bleue
])
</script>

<template>
  <!-- Liste des détails du produit -->
  <ul>
    <!-- Boucle pour afficher chaque détail -->
    <li v-for="detail in details">
      {{ detail }} <!-- Affiche le détail -->
    </li>
  </ul>

  <hr> <!-- Séparateur visuel -->

  <!-- Liste des variantes du produit -->
  <ul>
    <!-- Sous-liste pour les variantes -->
    <ul>
      <!-- Boucle pour afficher chaque variante -->
      <li v-for="variant in variants" :key="variant.id">
        {{ variant.color }} <!-- Affiche la couleur de la variante -->
      </li>
    </ul>
  </ul>
</template>
