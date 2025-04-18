<template>
  <div class="app">
    <div class="todo-container">
      <form @submit.prevent="addTodo" class="todo-form">
        <input v-model="newTodo" placeholder="Add a task..." />
        <button type="submit">Add</button>
      </form>

      <div class="filters">
        <button
          v-for="filter in ['all', 'complete', 'incomplete']"
          :key="filter"
          :class="{ active: currentFilter === filter }"
          @click="currentFilter = filter"
        >
          {{ filterLabel(filter) }}
        </button>
      </div>

      <ul class="todo-list">
        <li
          v-for="(todo, index) in filteredTodos"
          :key="index"
          class="todo-item"
        >
          <span
            :class="{ completed: todo.completed }"
            @click="toggleTodo(index)"
          >
            {{ todo.text }}
          </span>
          <div class="actions">
            <span class="circle" @click="toggleTodo(index)">
              {{ todo.completed ? '◉' : '◯' }}
            </span>
            <span class="trash" @click="removeTodo(index)">🗑️</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTodo = ref('')
const todos = ref([
  { text: 'test', completed: false },
  { text: 'Learn Vue 3', completed: true },
  { text: 'Learn Angular', completed: true },
  { text: 'Learn CSS 3', completed: false }
])

const currentFilter = ref('all')

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.unshift({ text: newTodo.value.trim(), completed: false })
    newTodo.value = ''
  }
}

const removeTodo = index => {
  todos.value.splice(index, 1)
}

const toggleTodo = index => {
  todos.value[index].completed = !todos.value[index].completed
}

const filteredTodos = computed(() => {
  if (currentFilter.value === 'complete') return todos.value.filter(t => t.completed)
  if (currentFilter.value === 'incomplete') return todos.value.filter(t => !t.completed)
  return todos.value
})

const filterLabel = (filter) => {
  const count = {
    all: todos.value.length,
    complete: todos.value.filter(t => t.completed).length,
    incomplete: todos.value.filter(t => !t.completed).length,
  }
  return `${filter.toUpperCase()} - (${count[filter]})`
}
</script>

<style scoped>
/* Base styling */
body,
html {
  margin: 0;
  padding: 0;
  font-family: system-ui, sans-serif;
}

.app {
  background-color: #0f172a;
  color: #f8fafc;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

/* Container */
.todo-container {
  background-color: #1e293b;
  border-radius: 12px;
  padding: 30px;
  width: 100%;
  max-width: 500px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
}

/* Form */
.todo-form {
  display: flex;
  margin-bottom: 20px;
}

.todo-form input {
  flex: 1;
  padding: 10px;
  border: none;
  border-radius: 8px 0 0 8px;
  font-size: 1rem;
  background-color: #0f172a;
  color: white;
  border: 1px solid #334155;
}

.todo-form button {
  padding: 10px 20px;
  border: none;
  border-radius: 0 8px 8px 0;
  background-color: #f1f5f9;
  color: #0f172a;
  font-weight: bold;
  cursor: pointer;
}

/* Filters */
.filters {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.filters button {
  background: transparent;
  border: 1px solid #475569;
  color: #f8fafc;
  padding: 6px 14px;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.filters button.active,
.filters button:hover {
  background: #334155;
}

/* Todo List */
.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #334155;
  padding: 12px 16px;
  margin-bottom: 8px;
  border-radius: 8px;
  background: #0f172a;
}

.todo-item span {
  font-size: 1rem;
}

.todo-item .completed {
  text-decoration: line-through;
  opacity: 0.6;
}

/* Actions */
.actions {
  display: flex;
  align-items: center;
  gap: 10px;
}

.circle {
  cursor: pointer;
  font-size: 1.2rem;
}

.trash {
  cursor: pointer;
  font-size: 1.2rem;
}
</style>
