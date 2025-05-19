<script setup>
import { ref, computed } from 'vue';

const status = ref('active');
const tasks = ref(['Task One', 'Task Two', 'Task Three', 'Task Four']);
const newTask = ref('');

// -Gestion du cycle de statuts
const toggleStatus = () => {
  const statusOrder = ['active', 'pending', 'inactive'];
  const currentIndex = statusOrder.indexOf(status.value);
  status.value = statusOrder[(currentIndex + 1) % statusOrder.length];
};

// -Ajout de tâche avec vérification
const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push(newTask.value.trim());
    newTask.value = '';
  }
};

// -Suppression de tâche
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

// -Calcul des tâches filtrées selon le statut
const filteredTasks = computed(() => {
  switch(status.value) {
    case 'pending': 
      return tasks.value.filter((_, index) => index % 2 === 0);
    case 'inactive':
      return [];
    default:
      return tasks.value;
  }
});
</script>

<template>
  <div class="p-17 space-y-4">
    <!-- Toggle Status -->
    <div class="flex items-center space-x-4">
      <button 
        @click="toggleStatus"
        class="px-4 py-2 rounded-md text-white"
        :class="{
          'bg-green-500': status === 'active',
          'bg-yellow-500': status === 'pending',
          'bg-gray-500': status === 'inactive'
        }"
      >
        Statut: {{ status }}
      </button>
      <span class="text-lg font-medium">
        {{ 
          status === 'active' ? 'Toutes les tâches' :
          status === 'pending' ? 'Tâches prioritaires' :
          'Aucune tâche visible'
        }}
      </span>
    </div>

    <!-- Ajout de tâche -->
    <form @submit.prevent="addTask" class="bg-white p-4 rounded-lg shadow">
      <label for="newTask" class="block text-lg mb-2">Nouvelle tâche:</label>
      <div class="flex space-x-2">
        <input
          id="newTask"
          v-model="newTask"
          type="text"
          class="flex-1 border border-gray-300 rounded-md px-3 py-2"
          placeholder="Entrez une nouvelle tâche"
        >
        <button
          type="submit"
          class="px-4 py-2 bg-blue-500 text-white rounded-md hover:bg-blue-600 transition"
          :disabled="!newTask.trim()"
        >
          Ajouter
        </button>
      </div>
    </form>

    <!-- Liste des tâches -->
    <ul v-if="filteredTasks.length" class="divide-y divide-gray-200">
      <li 
        v-for="(task, index) in filteredTasks" 
        :key="index"
        class="py-3 flex justify-between items-center"
      >
        <span>{{ task }}</span>
        <button
          @click="deleteTask(tasks.indexOf(task))"
          class="px-3 py-1 bg-red-500 text-white rounded-md hover:bg-red-600 transition"
        >
          Supprimer
        </button>
      </li>
    </ul>

    <!-- Message vide -->
    <div v-else class="text-center py-8 text-gray-500">
      Aucune tâche à afficher
    </div>
  </div>
</template>
