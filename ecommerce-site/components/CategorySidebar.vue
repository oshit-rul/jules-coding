<template>
  <aside class="w-1/4 p-4 bg-gray-100 rounded-lg shadow">
    <h3 class="text-xl font-semibold mb-4 text-gray-700">Categories</h3>
    <ul v-if="categories.length" class="space-y-2">
      <li v-for="category in categories" :key="category.id">
        <NuxtLink :to="`/categories/${category.slug}`" class="text-blue-600 hover:text-blue-800 hover:underline">
          {{ category.name }}
        </NuxtLink>
      </li>
    </ul>
    <p v-else class="text-gray-500">Loading categories...</p>
  </aside>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const categories = ref([]);

onMounted(async () => {
  try {
    // In Nuxt 3, useFetch is preferred for data fetching for SSR benefits.
    // This direct fetch works for client-side rendering or if /storage/* is publicly available.
    const response = await fetch('/storage/categories.json');
    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
    categories.value = await response.json();
  } catch (error) {
    console.error("Failed to load categories:", error);
    // Handle error appropriately in a real app (e.g., show a message to the user)
  }
});
</script>
