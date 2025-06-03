<template>
  <div class="max-w-3xl mx-auto p-6 bg-white rounded-lg shadow-md">
    <h1 v-if="faqData.title" class="text-4xl font-bold mb-8 text-center text-gray-800">{{ faqData.title }}</h1>
    <div v-if="!loading && faqData.faqs && faqData.faqs.length" class="space-y-6">
      <details v-for="faq in faqData.faqs" :key="faq.id" class="p-4 border rounded-lg shadow-sm hover:shadow-md transition-shadow bg-gray-50">
        <summary class="font-semibold text-lg cursor-pointer text-blue-700 hover:text-blue-900">{{ faq.question }}</summary>
        <p class="mt-2 text-gray-700 prose" v-html="faq.answer"></p> <!-- Assuming answer might contain HTML -->
      </details>
    </div>
    <p v-else-if="!loading" class="text-center text-red-500">No FAQs found or failed to load.</p>
    <p v-if="loading" class="text-gray-500 text-center">Loading FAQs...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const faqData = ref({});
const loading = ref(true);

onMounted(async () => {
  try {
    const response = await fetch('/storage/faq.json');
    if (!response.ok) throw new Error('Failed to fetch FAQ data');
    faqData.value = await response.json();
  } catch (error) {
    console.error("Error fetching FAQ page data:", error);
    faqData.value = { title: 'Error' }; // Provide fallback
  } finally {
    loading.value = false;
  }
});
</script>
