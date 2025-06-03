<template>
  <div class="prose max-w-none mx-auto p-6 bg-white rounded-lg shadow-md">
    <h1 v-if="aboutContent.title" class="text-4xl font-bold mb-6 text-gray-800">{{ aboutContent.title }}</h1>
    <div v-if="aboutContent.content" v-html="aboutContent.content" class="text-gray-700"></div>
    <div v-if="aboutContent.team_members && aboutContent.team_members.length" class="mt-8">
      <h2 class="text-2xl font-semibold mb-4 text-gray-700">Our Team</h2>
      <ul class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <li v-for="member in aboutContent.team_members" :key="member.name" class="bg-gray-50 p-4 rounded-lg shadow">
          <h3 class="text-xl font-medium text-blue-600">{{ member.name }}</h3>
          <p class="text-gray-600">{{ member.position }}</p>
        </li>
      </ul>
    </div>
    <p v-else-if="!aboutContent.title && !loading" class="text-center text-red-500">Failed to load content.</p>
    <p v-if="loading" class="text-gray-500 text-center">Loading about us information...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const aboutContent = ref({});
const loading = ref(true);

onMounted(async () => {
  try {
    const response = await fetch('/storage/about.json');
    if (!response.ok) throw new Error('Failed to fetch about content');
    aboutContent.value = await response.json();
  } catch (error) {
    console.error("Error fetching about page data:", error);
    aboutContent.value = { title: 'Error', content: 'Could not load content.' }; // Provide fallback content
  } finally {
    loading.value = false;
  }
});
</script>
<style scoped>
/* The 'prose' class from @tailwindcss/typography provides nice defaults. */
/* If not installed, these styles would be more basic. */
</style>
