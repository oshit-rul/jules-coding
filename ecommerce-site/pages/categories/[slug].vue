<template>
  <div class="p-6">
    <NuxtLink to="/categories" class="text-blue-600 hover:underline mb-6 block">&larr; Back to All Categories</NuxtLink>
    <h1 class="text-3xl font-bold mb-8 text-gray-800">
      Products in <span class="text-blue-600">{{ categoryName || $route.params.slug }}</span>
    </h1>
    <div v-if="!loading && products.length" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <ProductCard v-for="product in products" :key="product.id" :product="product" />
    </div>
    <p v-else-if="!loading && !products.length" class="text-center text-gray-600 py-8">No products found in this category.</p>
    <p v-if="loading" class="text-gray-500 text-center">Loading products...</p>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';
import ProductCard from '~/components/ProductCard.vue';

const route = useRoute();
const products = ref([]);
const allCategories = ref([]); // To store all categories for finding the name
const loading = ref(true);
const categorySlug = computed(() => route.params.slug);

const categoryName = computed(() => {
  const foundCategory = allCategories.value.find(cat => cat.slug === categorySlug.value);
  return foundCategory ? foundCategory.name : categorySlug.value;
});

onMounted(async () => {
  loading.value = true;
  try {
    // Fetch both products and categories data
    const [productsResponse, categoriesResponse] = await Promise.all([
      fetch('/storage/products.json'),
      fetch('/storage/categories.json')
    ]);

    if (!productsResponse.ok) throw new Error('Failed to fetch products');
    const allProducts = await productsResponse.json();

    if (!categoriesResponse.ok) throw new Error('Failed to fetch categories');
    allCategories.value = await categoriesResponse.json();

    // Filter products for the current category slug
    products.value = allProducts.filter(p => p.category_slug === categorySlug.value);
  } catch (error) {
    console.error(`Error fetching products for category ${categorySlug.value}:`, error);
    products.value = []; // Clear products on error
  } finally {
    loading.value = false;
  }
});
</script>
