<script setup>
/**
 * COMPOSANT : -Compteur interactif
 * Fonctionnalité : Gère un compteur avec incrémentation/décrémentation
 * et affichage conditionnel basé sur la valeur
 */

import { ref } from 'vue'

// Référence réactive pour le compteur (valeur initiale = 0)
const count = ref(0)

/**
 * Incrémente le compteur de +1
 * @function
 * @example
 * // Avant : count = 2
 * increment()
 * // Après : count = 3
 */
const increment = () => {
  count.value += 1
}
const reset = () => {
  count.value =0
}

/**
 * Décrémente le compteur de -1 (si > 0)
 * @function
 * @example
 * // Avant : count = 3
 * decrement()
 * // Après : count = 2
 */
const decrement = () => {
  if (count.value > 0) {
    count.value -= 1
  }
}
</script>

<template>
  <!-- Conteneur principal centré -->
  <div class="text-center grid justify-center items-center">
    
    <!-- Titre du compteur avec couleur conditionnelle -->
    <!-- Accessibilité : annonce les changements  -->

    <h1 
      class="text-center" 
      :style="{ color: count > 10 ? 'blue' : '' }"
      aria-live="polite" 
    >
      Compteur {{ count }}
    </h1>

    <!-- Messages conditionnels -->
    <!-- Niveau Élevé (≥5) -->
    <div v-if="count >= 5" class="text-green-700 pl-12">
      OK++++>>>>>>>>>>>>>> <!-- Indicateur visuel positif -->
    </div>
    
    <!-- Niveau Moyen (0<x<5) -->
    <div v-else-if="count > 0 && count < 5" class="text-red-700 pl-12">
      OK----<<<<<<<<<<<<<<<<< <!-- Indicateur visuel d'avertissement -->
    </div>
    
    <!-- Niveau Critique (≤0) -->
    <div v-else class="text-orange-400 pl-12">
      OK00000000000000000000 <!-- Indicateur visuel neutre/désactivé -->
    </div>

    <!-- Boutons de contrôle -->
    <div>
      <!-- Bouton Incrément (toujours actif) -->
      <button 
        @click="increment" 
        class="button"
        aria-label="Augmenter le compteur"
      >
        Increment
      </button>
      
      <!-- Bouton Décrément (conditionnel) -->
      <button
        @click="decrement"
        :disabled="count <= 0"
        :class="{ 
          'opacity-50 bg-red-200 cursor-not-allowed': count <= 1,
          'hover:bg-red-300': count > 1
        }"
        class="button transition-colors"
        aria-label="Diminuer le compteur"
      >
        Decrement
      </button>
      <button
        @click="reset"
        class="button transition-colors"
      >
       Reset
      </button>
    </div>
  </div>
</template>

<style scoped>
/* Styles isolés au composant */
/* .button {
  @apply px-3 py-2 mx-2 rounded-md bg-blue-500 text-white;
} */

/* .button:hover:not(:disabled) {
  @apply bg-blue-600;
} */
</style>
