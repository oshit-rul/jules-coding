<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.done" @change="toggleTodo" />
    <span :class="{ done: todo.done }">{{ todo.text }}</span>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

interface Todo {
  id: number;
  text: string;
  done: boolean;
}

const props = defineProps<{
  todo: Todo;
}>();

const emit = defineEmits(['toggle', 'delete']);

const toggleTodo = () => {
  emit('toggle', props.todo.id);
};

const deleteTodo = () => {
  emit('delete', props.todo.id);
};
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 0.75rem; /* Slightly increased gap */
  padding: 0.75rem 0.5rem; /* Adjusted padding */
  border-bottom: 1px solid #eee; /* Separator line */
  transition: background-color 0.2s ease;
}

.todo-item:last-child {
  border-bottom: none; /* No border for the last item */
}

.todo-item:hover {
  background-color: #f9f9f9; /* Slight hover effect */
}

.todo-item input[type="checkbox"] {
  cursor: pointer;
  width: 18px; /* Custom size */
  height: 18px; /* Custom size */
}

.todo-item span {
  flex-grow: 1; /* Text takes available space */
  font-size: 1rem;
  transition: color 0.2s ease;
}

.done {
  text-decoration: line-through;
  color: #999; /* Darker grey for completed items */
}

.todo-item button {
  background-color: #e74c3c; /* Red for delete */
  color: white;
  border: none;
  padding: 0.35rem 0.75rem; /* Adjusted padding */
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  opacity: 0.8;
  transition: opacity 0.2s ease, background-color 0.2s ease;
}

.todo-item button:hover {
  background-color: #c0392b; /* Darker red on hover */
  opacity: 1;
}
</style>
