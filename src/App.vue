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
</script>

<template>
  <div>
    <u>
      <li v-for="task in tasks" :key="task.id">
        {{ task.title }} - {{ task.completed }}
      </li>
    </u>
  </div>
</template>

<style scoped>

</style>
