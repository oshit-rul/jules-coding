<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-8 text-gray-800">All Categories</h1>
    <div v-if="!loading && categories.length" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <NuxtLink v-for="category in categories" :key="category.id" :to="`/categories/${category.slug}`"
                class="block p-6 bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow text-center hover:bg-blue-50">
        <h2 class="text-xl font-semibold text-blue-700">{{ category.name }}</h2>
      </NuxtLink>
    </div>
    <p v-else-if="!loading" class="text-center text-gray-500">No categories found.</p>
    <p v-if="loading" class="text-gray-500 text-center">Loading categories...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const categories = ref([]);
const loading = ref(true);

onMounted(async () => {
  try {
    const response = await fetch('/storage/categories.json');
    if (!response.ok) throw new Error('Failed to fetch categories');
    categories.value = await response.json();
  } catch (error) {
    console.error("Error fetching categories list:", error);
  } finally {
    loading.value = false;
  }
});
</script>
