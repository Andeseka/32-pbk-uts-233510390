<template>
  <div class="container">
    <div class="terminal">
      <span>M. Andeseka Satria DS</span>
    </div>

    <h1 class="title">📝 Daftar Kegiatan</h1>

    <div class="input-wrapper">
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        class="input"
        placeholder="Tambah kegiatan..."
      />
      <button @click="addTask" class="btn-add">+</button>
    </div>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showIncompleteOnly" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul class="task-list">
      <li
        v-for="(task, index) in filteredTasks"
        :key="index"
        class="task-item"
      >
        <div class="task-check">
          <input type="checkbox" v-model="task.done" />
          <span :class="{ done: task.done }">{{ task.text }}</span>
        </div>
        <button class="btn-delete" @click="deleteTask(index)">✕</button>
      </li>
    </ul>

    <div v-if="filteredTasks.length === 0" class="empty-msg">
      Tidak ada kegiatan yang ditampilkan.
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      showIncompleteOnly: false
    };
  },
  computed: {
    filteredTasks() {
      return this.showIncompleteOnly
        ? this.tasks.filter(task => !task.done)
        : this.tasks;
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask.trim(), done: false });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>
