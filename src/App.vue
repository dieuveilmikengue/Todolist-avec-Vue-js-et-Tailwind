<template>
 <div id="app" class="container mx-auto px-4 py-8 max-w-2xl">
    <!-- En-tête personnalisée -->
    <header class="mb-8 text-center">
      <h1 class="text-3xl font-bold text-indigo-600">Salut ! {{ firstName }}</h1>
      <p class="text-gray-500 mt-2">Gère ta liste de films préférés</p>
    </header>

    <!-- Formulaire d'ajout -->
    <form @submit.prevent="addMovie" class="mb-8 bg-white p-6 rounded-xl shadow-sm">
      <div class="flex gap-2">
        <input
          v-model="movieName"
          type="text"
          placeholder="Nouveau film"
          class="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500"
          required
        >
        <button
          type="submit"
          class="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition-colors flex items-center gap-2"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
          </svg>
          Ajouter
        </button>
      </div>
      <p v-if="movieName" class="text-sm text-gray-500 mt-2">Prêt à ajouter : <span class="font-medium">{{ movieName }}</span></p>
    </form>

    <!-- Liste des films -->
    <div class="bg-white rounded-xl shadow-sm overflow-hidden">
      <ul v-if="movies.length" class="divide-y divide-gray-200">
        <li
          v-for="movie in movies"
          :key="movie"
          class="px-6 py-4 flex justify-between items-center hover:bg-gray-50 transition-colors"
        >
          <span class="font-medium text-gray-800">{{ movie }}</span>
          <button
            @click="deleteMovie(movie)"
            class="p-2 text-red-500 hover:text-red-700 transition-colors"
            title="Supprimer"
          >
            <i class="fas fa-trash-alt"></i>
          </button>
        </li>
      </ul>
      <div v-else class="p-6 text-center text-gray-500">
        Aucun film dans votre liste. Ajoutez-en un !
      </div>
    </div>
  </div>
</template>

<script setup>


  import { ref } from 'vue'

  const movieName = ref("")

  const firstName = "Mike"

  const movies = ref([])


  const deleteMovie = (movie) => {
    movies.value = movies.value.filter(m => m !== movie)
  }


  const addMovie = () => {
    event.preventDefault()
    movies.value.push(movieName.value)
    movieName.value = ""
  }
</script>