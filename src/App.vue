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
  <div class="flex p-6 min-h-screen bg-gray-900 text-white gap-6 items-center">
    <!-- Sidebar -->
    <div class="flex flex-col w-[320px] h-full bg-gray-800 rounded-lg shadow-xl p-6 gap-6">
      <h1 class="text-center text-3xl font-bold tracking-wide">📋 Task Manager</h1>

      <!-- Input -->
      <div class="flex items-center gap-4">
        <input
          type="text"
          v-model="newTask"
          @keyup.enter="addTask"
          placeholder="New task..."
          class="flex-1 px-4 py-2 rounded bg-gray-700 border border-gray-600 focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        <button
          @click="addTask"
          class="bg-blue-600 hover:bg-blue-700 transition px-4 py-2 rounded shadow text-white"
        >
          ➕
        </button>
      </div>

      <!-- Filter -->
      <div class="flex flex-col gap-2">
        <button
          @click="filter = 'all'"
          class="bg-gray-700 hover:bg-gray-600 rounded px-4 py-2 transition"
        >
          ☰ Semua
        </button>
        <button
          @click="filter = 'active'"
          class="bg-gray-700 hover:bg-gray-600 rounded px-4 py-2 transition"
        >
          🕒 Active
        </button>
        <button
          @click="filter = 'completed'"
          class="bg-gray-700 hover:bg-gray-600 rounded px-4 py-2 transition"
        >
          ✅ Completed
        </button>
      </div>
    </div>

    <!-- Task List -->
    <div class="flex-1 h-130 bg-gray-800 rounded-lg shadow-xl p-6 overflow-hidden">
      <h2 class="text-2xl font-semibold mb-4">📝 Daftar Tugas</h2>
      <ul class="space-y-4 h-100 overflow-y-auto pr-2">
        <li
          v-for="task in filteredTasks"
          :key="task.id"
          class="flex items-center justify-between bg-gray-700 p-4 rounded transition-transform duration-300 hover:scale-[1.01]"
        >
          <div class="flex items-center gap-3">
            <input
              type="checkbox"
              v-model="task.completed"
              class="w-5 h-5 accent-green-500"
            />
            <span
              :class="task.completed ? 'line-through text-gray-400' : 'text-white'"
              class="text-lg"
            >
              {{ task.title }}
            </span>
          </div>
          <button
            @click="removeTask(task)"
            class="text-red-400 hover:text-red-600 transition"
            title="Remove"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="2"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
/* Tambahan animasi masuk jika ingin */
li {
  animation: fadeIn 0.4s ease-in-out;
}
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(6px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>