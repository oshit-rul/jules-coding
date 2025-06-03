<template>
  <div class="flex flex-col min-h-screen">
    <AppHeader />
    <main class="flex-grow container mx-auto py-8 px-4">
      <NuxtPage />
    </main>
    <AppFooter />
  </div>
</template>

<script setup>
import AppHeader from '~/components/AppHeader.vue';
import AppFooter from '~/components/AppFooter.vue';
</script>

<style>
body {
  @apply bg-gray-50 text-gray-800; /* Slightly lighter bg and darker text */
}
/* Example of a global style, could also be in assets/css/main.css */
.container {
  max-width: 1280px; /* Standard container width */
}
</style>
