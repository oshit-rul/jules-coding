<template>
  <div class="p-6 bg-white rounded-lg shadow-md max-w-2xl mx-auto">
    <h1 v-if="contactInfo.title" class="text-4xl font-bold mb-8 text-center text-gray-800">{{ contactInfo.title }}</h1>
    <div v-if="!loading && contactInfo.email" class="space-y-6">
      <p class="text-lg text-gray-700"><strong class="font-semibold text-gray-900">Email:</strong> <a :href="'mailto:' + contactInfo.email" class="text-blue-600 hover:underline">{{ contactInfo.email }}</a></p>
      <p class="text-lg text-gray-700"><strong class="font-semibold text-gray-900">Phone:</strong> {{ contactInfo.phone }}</p>
      <p class="text-lg text-gray-700"><strong class="font-semibold text-gray-900">Address:</strong> {{ contactInfo.address }}</p>
      <div v-if="contactInfo.map_embed_url" class="mt-6">
        <h2 class="text-2xl font-semibold mb-3 text-gray-700">Our Location</h2>
        <iframe :src="contactInfo.map_embed_url" width="100%" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade" class="rounded-md shadow"></iframe>
      </div>
    </div>
    <p v-else-if="!loading" class="text-center text-red-500">Failed to load contact information.</p>
    <p v-if="loading" class="text-gray-500 text-center">Loading contact information...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const contactInfo = ref({});
const loading = ref(true);

onMounted(async () => {
  try {
    const response = await fetch('/storage/contact.json');
    if (!response.ok) throw new Error('Failed to fetch contact info');
    contactInfo.value = await response.json();
  } catch (error) {
    console.error("Error fetching contact page data:", error);
    contactInfo.value = { title: 'Error' }; // Provide fallback
  } finally {
    loading.value = false;
  }
});
</script>
