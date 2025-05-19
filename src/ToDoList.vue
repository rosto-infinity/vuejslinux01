<script setup>
import { ref } from 'vue'

// -Déclare une référence réactive pour stocker les couleurs
const colors = ref(["Red", "Green", "Blue", "Gray"])

// -Fonction pour supprimer une couleur de la liste
const deleteColor = (color) => {
  // -Met à jour la liste des couleurs en filtrant celle à supprimer
  colors.value = colors.value.filter(
    col => col !== color // -Inclut uniquement les couleurs qui ne correspondent pas à celle à supprimer
  )
}

// -Fonction pour trier les couleurs en ordre alphabétique
const sortColors = () => {
  // --Trie le tableau des couleurs
  colors.value.sort((a, b) => a > b ? 1 : -1) // Compare les couleurs pour le tri
}

// -Déclare une référence réactive pour le nom de la nouvelle couleur
const newColor = ref('')

// -Déclare une référence pour les nouvelles couleurs (non utilisée ici)


// -Fonction pour ajouter une nouvelle couleur à la liste
const addColor = () => {
  // -Ajoute la nouvelle couleur à la liste des couleurs
  colors.value.push(newColor.value)
  // --Réinitialise le champ de saisie
  newColor.value = ''
}
</script>

<template>
  <div class="p-17">
    <!-- Formulaire pour ajouter une nouvelle couleur -->
     <!-- -Lie le champ de saisie à la référence newColor -->
    <form action="" @submit.prevent="addColor">
      <input 
        v-model="newColor" 
        class="border-2 border-green-400 p-3 rounded-md"
        type="text" 
        placeholder="Nouvelle couleur" 
      >
      <button
       :disabled="newColor.length == 0"
      class="bg-green-force px-7 rounded-md py-2 disabled:opacity-50 disabled:cursor-not-allowed">Ajouter</button> <!-- Bouton pour ajouter la couleur -->
    </form>
    
    <!-- Bouton pour réorganiser la liste des couleurs -->
     <!-- Appelle la méthode sortColors lors du clic -->
    <button 
      @click="sortColors" 
      class="button">Réorganiser</button>

    <!-- Liste des couleurs -->
    <ul class="pl-9 pt-10">
      <li v-for="color in colors" :key="color"> <!-- Itère sur chaque couleur dans colors -->
        {{ color }} <!-- Affiche le nom de la couleur -->
        <!-- Appelle deleteColor pour supprimer la couleur -->
        <button
       
          @click="deleteColor(color)" 
          class="px-3 py-0.5 rounded-md bg-amber-700 my-2 cursor-pointer" 
          type="button">Supprimer
        </button> <!-- Bouton pour supprimer la couleur -->
      </li>
    </ul>
  </div>
</template>

<style scoped>
.bg-green-force {
    background-color: #0de270 !important; /* Couleur verte de Tailwind, forcée avec !important */
    cursor: pointer;
}
</style>
