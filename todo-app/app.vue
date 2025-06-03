<template>
  <div id="app-container">
    <NuxtRouteAnnouncer />
    <header>
      <h1>My Todo App</h1>
    </header>
    <main>
      <TodoList />
    </main>
    <footer>
      <p>&copy; 2024 Todo App</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import TodoList from '~/components/TodoList.vue';
</script>

<style>
/* Global Styles */
body {
  font-family: 'Helvetica Neue', Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #eef1f5; /* Lighter, softer background */
  color: #333;
  line-height: 1.6;
}

#app-container {
  max-width: 800px; /* Max width for the whole app content */
  margin: 0 auto; /* Center the app container */
  padding: 1rem;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

header {
  background-color: #4a90e2; /* A pleasant blue */
  color: white;
  padding: 1rem 0;
  text-align: center;
  border-radius: 8px 8px 0 0; /* Rounded corners for top */
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

header h1 {
  margin: 0;
  font-size: 2rem;
  font-weight: 500;
}

main {
  flex-grow: 1; /* Ensures main content takes available space */
  padding: 1rem 0; /* Add some padding top and bottom */
}

footer {
  text-align: center;
  padding: 1rem 0;
  font-size: 0.9rem;
  color: #777;
  border-top: 1px solid #ddd;
  margin-top: 2rem;
}
</style>
