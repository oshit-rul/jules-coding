<template>
  <div class="todo-list">
    <h2>Todo List</h2>
    <div class="add-todo">
      <input type="text" v-model="newTodoText" placeholder="Add a new todo" @keyup.enter="addTodo" />
      <button @click="addTodo">Add</button>
    </div>
    <div v-if="todos.length === 0" class="empty-state">
      No todos yet. Add one above!
    </div>
    <div v-else>
      <Todo v-for="todo in todos" :key="todo.id" :todo="todo" @toggle="toggleTodo" @delete="deleteTodo" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import Todo from './Todo.vue'; // Import the Todo component

interface TodoItem {
  id: number;
  text: string;
  done: boolean;
}

const todos = ref<TodoItem[]>([]);
const newTodoText = ref('');
let nextId = 0;

const addTodo = () => {
  if (newTodoText.value.trim() === '') {
    return; // Do not add empty todos
  }
  todos.value.push({
    id: nextId++,
    text: newTodoText.value,
    done: false,
  });
  newTodoText.value = ''; // Clear input after adding
};

const toggleTodo = (id: number) => {
  const todo = todos.value.find(t => t.id === id);
  if (todo) {
    todo.done = !todo.done;
  }
};

const deleteTodo = (id: number) => {
  todos.value = todos.value.filter(t => t.id !== id);
};
</script>

<style scoped>
.todo-list {
  background-color: #ffffff; /* White background for the card */
  padding: 1.5rem; /* Increased padding */
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Softer, deeper shadow */
  margin-top: 1rem; /* Space from header */
}

.todo-list h2 {
  text-align: center;
  color: #333;
  margin-top: 0; /* Remove default margin */
  margin-bottom: 1.5rem; /* Space below heading */
  font-weight: 600;
}

.add-todo {
  display: flex;
  gap: 0.75rem; /* Slightly increased gap */
  margin-bottom: 1.5rem; /* Increased space below add section */
}

.add-todo input[type="text"] {
  flex-grow: 1;
  padding: 0.75rem; /* Increased padding */
  border: 1px solid #ccc;
  border-radius: 6px; /* Slightly more rounded */
  font-size: 1rem;
}

.add-todo input[type="text"]:focus {
  outline: none;
  border-color: #4a90e2; /* Blue border on focus */
  box-shadow: 0 0 0 2px rgba(74, 144, 226, 0.2);
}

.add-todo button {
  padding: 0.75rem 1.25rem; /* Increased padding */
  background-color: #5cb85c; /* Green for add button */
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.2s ease;
}

.add-todo button:hover {
  background-color: #4cae4c; /* Darker green on hover */
}

.empty-state {
  text-align: center;
  color: #666; /* Slightly darker for better readability */
  margin-top: 2rem; /* More space for empty state */
  font-style: italic;
}

/* Styling for the list of todos */
.todos-container {
  margin-top: 1rem;
}
</style>
