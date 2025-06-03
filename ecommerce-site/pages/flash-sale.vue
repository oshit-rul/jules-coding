<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-8 text-center text-red-600 bg-yellow-200 p-4 rounded-lg shadow-md">
      <span class="animate-pulse">⚡ Flash Sale! ⚡</span>
    </h1>
    <div v-if="!loading && flashSaleProducts.length" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <ProductCard v-for="product in flashSaleProducts" :key="product.id" :product="product" />
    </div>
    <p v-else-if="!loading" class="text-center text-gray-600 py-8">No products currently in flash sale. Check back soon!</p>
    <p v-if="loading" class="text-gray-500 text-center">Loading flash sale products...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import ProductCard from '~/components/ProductCard.vue';

const flashSaleProducts = ref([]);
const loading = ref(true);

onMounted(async () => {
  loading.value = true;
  try {
    const response = await fetch('/storage/products.json');
    if (!response.ok) throw new Error('Failed to fetch products');
    const allProducts = await response.json();
    flashSaleProducts.value = allProducts.filter(p => p.flash_sale);
  } catch (error) {
    console.error("Error fetching flash sale products:", error);
    flashSaleProducts.value = []; // Clear on error
  } finally {
    loading.value = false;
  }
});
</script>
