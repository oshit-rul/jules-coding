<template>
  <header class="bg-blue-600 text-white p-4 shadow-md">
    <nav class="container mx-auto flex justify-between items-center">
      <NuxtLink to="/" class="text-2xl font-bold">MyShop</NuxtLink>
      <ul class="flex space-x-4">
        <li><NuxtLink to="/about" class="hover:text-blue-200">About Us</NuxtLink></li>
        <li><NuxtLink to="/contact" class="hover:text-blue-200">Contact Us</NuxtLink></li>
        <li><NuxtLink to="/faq" class="hover:text-blue-200">FAQ</NuxtLink></li>
        <li><NuxtLink to="/categories" class="hover:text-blue-200">Categories</NuxtLink></li>
        <li><NuxtLink to="/flash-sale" class="hover:text-blue-200">Flash Sale</NuxtLink></li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
</script>
