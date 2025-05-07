<template>
<div class="container">
    <h1>📝 My List</h1>

    <div class="input-wrapper">
      <input
        v-model="newTask"
        type="text"
        placeholder="Tambah kegiatan baru..."
      />
      <input
        v-model="newStartTime"
        type="time"
        class="time-input"
      />
      <span>→</span>
      <input
        v-model="newEndTime"
        type="time"
        class="time-input"
      />
      <button @click="addTask" class="add">
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
        </svg>
        <span>Tambah</span>
      </button>
    </div>
    <button @click="showCompleted = !showCompleted" class="toggle">
      {{ showCompleted ? 'Hanya Belum Selesai' : 'Tampilkan Semua' }}
    </button>

    <div class="task-list">
      <div
        v-for="(task, index) in filteredTasks"
        :key="index"
        :class="['task', { completed: task.completed }]"
      >
        <input type="checkbox" v-model="task.completed" />
        <div class="task-text" :class="{ completed: task.completed }">
          {{ task.text }}
          <div v-if="task.startTime && task.endTime" class="due-time">
            🕒 {{ task.startTime }} - {{ task.endTime }}
          </div>
        </div>
        <button @click="deleteTask(index)" class="delete">Hapus</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const tasks = ref([]);
    const newTask = ref('');
    const newStartTime = ref('');
    const newEndTime = ref('');
    const showCompleted = ref(false);

    const addTask = () => {
      if (newTask.value.trim() && newStartTime.value && newEndTime.value) {
        tasks.value.push({
          text: newTask.value.trim(),
          completed: false,
          startTime: newStartTime.value,
          endTime: newEndTime.value
        });
        newTask.value = '';
        newStartTime.value = '';
        newEndTime.value = '';
      }
    };

    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
    };

    const filteredTasks = computed(() => {
      return showCompleted.value
        ? tasks.value
        : tasks.value.filter(task => !task.completed);
    });

    return {
      tasks,
      newTask,
      newStartTime,
      newEndTime,
      addTask,
      deleteTask,
      showCompleted,
      filteredTasks
    };
  }
};
</script>

<style>
body {
  font-family: 'Quicksand', 'Segoe UI', 'Inter', sans-serif;
  background-color: #f3f4f6;
  color: #111827;
}

.container {
  max-width: 640px;
  margin: 60px auto;
  padding: 32px;
  background-color: #ffffff;
  border-radius: 24px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.06);
}

h1 {
  font-size: 2.5rem;
  color: #2563eb;
  font-weight: 900;
  margin-bottom: 24px;
  
}

.input-wrapper {
  display: flex;
  gap: 8px;
  margin-bottom: 20px;
  align-items: center;
}

input[type="text"],
.time-input {
  flex: 1;
  padding: 10px 12px;
  font-size: 16px;
  border: 1px solid #d1d5db;
  border-radius: 12px;
  background-color: #f9fafb;
}
input[type="text"]:focus,
.time-input:focus {
  border-color: #2563eb;
  outline: none;
  background-color: #fff;
}

button.add {
  background-color: #2563eb;
  color: white;
  border: none;
  padding: 12px 16px;
  border-radius: 12px;
  font-weight: 600;
  font-size: 14px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 6px;
}

button.add:hover {
  background-color: #1e40af;
}
</style>
