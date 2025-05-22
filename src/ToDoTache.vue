<template>
  <div class="p-12">
    <h1>Listes des tâches</h1>

    <!-- -Formulaire pour ajouter une nouvelle tâche -->
    <form action="" @submit.prevent="addTodo">
      <input 
        v-model="newTodo" 
        type="text" 
        class="border-1 border-green-700 px-3 py-2"
        placeholder="Tâche à effectuer"
      >

      <!-- Bouton pour ajouter la tâche, désactivé si newTodo est vide -->
      <button 
        :disabled="newTodo.length == 0"
        class="px-7 border-1 border-green-700 py-2 bg-green-700 rounded-r-md text-green-100 hover:bg-green-800 mr-3 disabled:opacity-50 disabled:cursor-not-allowed"
      >
        Ajouter
      </button>

      <!-- Bouton pour réorganiser les tâches de A à Z -->
      <button 
        class="px-7 py-2 bg-green-900 rounded-md text-green-100 hover:bg-green-800 mr-3"
      >
        Réorganiser A🔄Z
      </button>
    </form>

    <!-- Message affiché lorsqu'il n'y a pas de tâches -->
    <div v-if="newTodo.length === 0" class="text-2xl mt-3">
      Vous n'avez pas de tâches à faire 😞
    </div>

    <!-- Liste des tâches -->
    <ul class="mt-5">
      <li 
        v-for="todo in todos" 
        :key="todo.date" 
        class="text-2xl"
      >
        <input type="checkbox" name="" id=""> {{ todo.title }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Référence pour le texte de la nouvelle tâche
const newTodo = ref('');

// Référence pour la liste des tâches
const todos = ref([]);

// Fonction pour ajouter une nouvelle tâche à la liste
const addTodo = () => {
  todos.value.push({
    title: newTodo.value,  // Titre de la nouvelle tâche
    completed: true,       // État de complétion initial (true par défaut, peut être ajusté plus tard)
    date: Date.now()       // Timestamp pour identifier de manière unique la tâche
  });
  
  newTodo.value = " "; // Réinitialise la nouvelle tâche (peut gérer la suppression ou une autre logique ici)
}
</script>

<style scoped>
/* Styles spécifiques peuvent être ajoutés ici */
</style>
