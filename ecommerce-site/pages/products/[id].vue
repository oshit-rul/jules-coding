<template>
  <div>
    <h1 class="text-3xl font-bold mb-6">Product Details: ID {{ $route.params.id }}</h1>
    <p>Detailed information for a single product will be displayed here, loaded from storage/products.json.</p>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
const route = useRoute();
// Logic to fetch product details based on route.params.id
</script>
