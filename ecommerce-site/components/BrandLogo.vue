<template>
  <div class="p-2 bg-gray-50 rounded-md shadow-sm flex items-center justify-center h-24">
    <img :src="brand.logo || '/images/brand_placeholder.png'" :alt="brand.name" class="max-h-full max-w-full object-contain">
  </div>
</template>

<script setup>
const props = defineProps({
  brand: {
    type: Object,
    required: true
  }
});
</script>
