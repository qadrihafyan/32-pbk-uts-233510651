<script setup>
import { ref, computed } from 'vue'

const tasks = ref([])
const newTask = ref('')
const filter = ref('all')

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

const removeTask = (task) => {
  tasks.value = tasks.value.filter(t => t.id !== task.id)
}

const filteredTasks = computed(() => {
  if (filter.value === 'completed') {
    return tasks.value.filter(task => task.completed)
  } else if (filter.value === 'active') {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})

</script>

<template>
  <div class="flex p-3 min-w-screen min-h-screen bg-amber-50">
    <!-- Left Content -->
    <div class="flex flex-col w-1/3 bg-white rounded-lg shadow-lg p-4 gap-5">
      <h1 class="w-full text-center text-2xl">Judul Header</h1>
      <div class="flex items-center justify-center gap-4 w-full">
        <input type="text" v-model="newTask" @keyup.enter="addTask" />
        <button @click="addTask">Add Task</button>
      </div>
      <div class="flex flex-col gap-5 mt-5 ">
        <button @click="filter = 'all'">Semua</button>
        <button @click="filter = 'active'">Active</button>
        <button @click="filter = 'completed'">Completed</button>
      </div>
    </div>

    <!-- Right Content -->
    <div>
      <ul>
        <li v-for="task in filteredTasks" :key="task.id">
          <input type="checkbox" v-model="task.completed" />
          <span :class="task.completed ? 'line-through text-gray-500' : ''">
            {{ task.title }} - {{ task.completed }}
          </span>
          <button @click="removeTask(task)">Remove</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
