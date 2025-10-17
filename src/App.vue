<template>
  <div class="p-4">
    <h1 class="text-3xl font-bold mb-4">Portal de Noticias</h1>

    <div v-if="loading">Cargando noticias...</div>
    <div v-else-if="error" class="text-red-500">{{ error }}</div>

    <div v-else class="grid gap-4 md:grid-cols-2 lg:grid-cols-3">
      <div v-for="(article, index) in articles" :key="index" class="p-4 border rounded shadow">
        <img
          v-if="article.urlToImage"
          :src="article.urlToImage"
          alt="imagen"
          class="w-full h-48 object-cover rounded"
        />
        <h3 class="text-lg font-semibold mt-2">{{ article.title }}</h3>
        <p class="text-sm text-gray-600">{{ article.source.name }}</p>
        <a :href="article.url" target="_blank" class="text-blue-600 hover:underline">
          Leer más
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const articles = ref([])   // array reactivo para las noticias
const loading = ref(true)   // estado de carga
const error = ref(null)     // estado de error

onMounted(async () => {
  try {
    const apiKey = import.meta.env.VITE_NEWS_API_KEY
    console.log('API Key:', apiKey) // para verificar que la clave se lee

    const response = await fetch(
      //`https://newsapi.org/v2/top-headlines?country=ar&apiKey=${apiKey}`
      `https://newsapi.org/v2/top-headlines?country=us&apiKey=${apiKey}`

    )

    if (!response.ok) throw new Error('Error al obtener noticias')

    const data = await response.json()
    console.log('Respuesta de la API:', data)
    articles.value = data.articles  // guardamos las noticias
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
})
</script>


