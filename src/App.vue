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
    </div>

</template>

<script>

</script>

<style>
</style>
