<script setup>
import { ref } from 'vue'

const tasks = ref([
  {
    id: 1,
    title: 'matmatics',
    completed: false
  },
  {
    id: 2,
    title: 'pemrograman',
    completed: false
  },
  {
    id: 3,
    title: 'bahasa inggris',
    completed: false
  }
])
const newTask = ref('')

const addTask = () => {
  if (newTask.value === '') {
    return
  }
  tasks.value.push({
    id: tasks.value.length + 1,
    title: newTask.value,
    completed: false
  })
  newTask.value = ''
  console.log(tasks.value)
}
</script>

<template>
  <div>
    <!-- Left Content -->
    <div>
      <input type="text" v-model="newTask" @keyup.enter="addTask" />
      <button @click="addTask">Add Task</button>
    </div>

    <!-- Right Content -->
    <div>
      <ul>
        <li v-for="task in tasks" :key="task.id">
          {{ task.title }} - {{ task.completed }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
