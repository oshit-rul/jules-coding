<template>
  <div class="border rounded-lg p-4 shadow-sm hover:shadow-md transition-shadow bg-white">
    <NuxtLink :to="`/products/${product.id}`">
      <img :src="product.image || '/images/placeholder.jpg'" :alt="product.name" class="w-full h-40 object-cover rounded mb-3">
      <h4 class="text-lg font-semibold text-gray-800 mb-1">{{ product.name }}</h4>
      <p class="text-gray-600 mb-2">{{ product.category_slug }}</p>
      <p class="text-xl font-bold text-blue-600">${{ product.price.toFixed(2) }}</p>
    </NuxtLink>
    <button @click="addToCart" class="mt-3 w-full bg-green-500 hover:bg-green-600 text-white py-2 px-4 rounded transition-colors">
      Add to Cart
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  product: {
    type: Object,
    required: true
  }
});

const addToCart = () => {
  console.log('Added to cart:', props.product.name);
  // Actual cart logic would be implemented here
};
</script>
