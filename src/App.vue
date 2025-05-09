<script setup>
import { ref } from 'vue'

const tasks = ref([])
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
          <input type="checkbox" v-model="task.completed"/>
          <span :class="task.completed ? 'line-through text-gray-500' : ''">
            {{ task.title }} - {{ task.completed }}
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
