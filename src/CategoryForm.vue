<template>
  <!-- -En-tête de section avec titre et fil d'Ariane -->
  <AppSectionHeader title="Categories" :bread-crumb="breadCrumb">
  </AppSectionHeader>

  <!-- -Carte principale contenant le formulaire -->
  <AppCard class="w-full md:w-3/4 xl:w-1/2">
      <!-- -Titre dynamique de la carte -->
      <template #title> {{ title }} </template>
      
      <template #content>
          <!-- -Affichage des erreurs de formulaire -->
          <AppFormErrors class="mb-4" />
          
          <!-- Formulaire principal -->
          <form class="pt-4">
              <!-- -Composants enfants pour chaque section du formulaire -->
              <CategoryBody />      <!-- xChamps de base (nom, description) -->
              <CategoryImage />     <!-- cUpload d'image -->
              <CategorySeo />       <!-- cMétadonnées SEO -->
              <CategoryVisibility /><!-- Paramètres de visibilité -->
          </form>
      </template>
      
      <!-- cPied de carte avec bouton de soumission -->
      <template #footer>
          <AppButton class="btn btn-primary" @click="submitForm">
              Save
          </AppButton>
      </template>
  </AppCard>
</template>

<script setup>
// Imports des dépendances
import { useForm } from '@inertiajs/vue3'  // cGestion de formulaires Inertia
import { onUnmounted } from 'vue'          // dCycle de vie Vue
import useTitle from '@/Composables/useTitle'          // fHook personnalisé pour les titres
import useFormContext from '@/Composables/useFormContext' // dHook pour le contexte du formulaire
import useCategoryStore from './CategoryStore'         // sddStore Pinia pour les catégories

// Imports des composants enfants
import CategoryBody from './Components/CategoryBody.vue'
import CategoryImage from './Components/CategoryImage.vue'
import CategorySeo from './Components/CategorySeo.vue'
import CategoryVisibility from './Components/CategoryVisibility.vue'

// cnitialisation du store Pinia
const categoryStore = useCategoryStore()

// Props : fréception d'une catégorie existante (pour édition)
const props = defineProps({
  category: {
      type: Object,
      default: null  // cNull signifie création d'une nouvelle catégorie
  }
})

// Si une catégorie existe, on l'hydrate dans le store
if (props.category) {
  categoryStore.setCategory(props.category)
}

// Nettoyage : réinitialisation du store quand le composant est détruit
onUnmounted(() => {
  categoryStore.$reset()
})

// Configuration du fil d'Ariane (breadcrumb)
const breadCrumb = [
  { label: 'Home', href: route('dashboard.index') },
  { label: 'Categories', href: route('blogCategory.index') },
  { label: 'Category', last: true } // Dernier élément non cliquable
]

// Gestion du titre dynamique
const { title } = useTitle('Category') // Génère "Create Category" ou "Edit Category"

// Vérification du contexte (création vs édition)
const { isCreate } = useFormContext()

// Soumission du formulaire
const submitForm = () => {
  const form = useForm(categoryStore.category) // Crée un objet form Inertia

  // Envoi différencié selon le contexte
  if (isCreate.value) {
      // Requête POST pour la création
      form.post(route('blogCategory.store'))
  } else {
      // Requête PUT masquée en POST pour la mise à jour
      form.transform((data) => ({
          ...data,
          _method: 'PUT' // Méthode spoofing pour les requêtes PUT/PATCH/DELETE
      })).post(route('blogCategory.update', props.category.id))
  }
}
</script>
