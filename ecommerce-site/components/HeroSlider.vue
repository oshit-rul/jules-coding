<template>
  <section class="bg-blue-500 text-white p-6 rounded-lg shadow-lg mb-8">
    <h2 class="text-2xl font-bold mb-4">Promotions</h2>
    <div v-if="promotions.length" class="space-y-3">
      <div v-for="promo in promotions" :key="promo.id" class="p-4 bg-blue-600 rounded">
        <NuxtLink :to="promo.link" class="hover:text-blue-200">
          <img :src="promo.image" :alt="promo.title" class="w-full h-48 object-cover rounded mb-2" v-if="promo.image">
          <h3 class="text-xl font-semibold">{{ promo.title }}</h3>
        </NuxtLink>
      </div>
    </div>
    <p v-else class="text-blue-100">Loading promotions...</p>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const promotions = ref([]);

onMounted(async () => {
  try {
    const response = await fetch('/storage/promotions.json');
    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
    promotions.value = await response.json();
  } catch (error) {
    console.error("Failed to load promotions:", error);
  }
});
</script>
