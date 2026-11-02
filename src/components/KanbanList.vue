<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  id: number
  title: string
  status: 'Backlog' | 'Doing' | 'Review' | 'Done'
}

// Beispiel-Aufgaben für das Board
const tasks = ref<Task[]>([
  { id: 1, title: 'Spring Boot Backend aufsetzen', status: 'Done' },
  { id: 2, title: 'Vue.js Frontend aufsetzen', status: 'Review' },
  { id: 3, title: 'v-for Komponente einbauen', status: 'Doing' },
  { id: 4, title: 'REST-Schnittstelle anbinden', status: 'Backlog' },
])

const columns = [
  { name: 'Backlog', color: '#9cdcdc' },
  { name: 'Doing', color: '#e67a7a' },
  { name: 'Review', color: '#ffe596' },
  { name: 'Done', color: '#dbe9b6' },
]
</script>

<template>
  <div class="board-container">
    <h1 class="board-title">Kanban Board</h1>

    <div class="board-columns">
      <div v-for="col in columns" :key="col.name" class="column">
        <div class="column-header" :style="{ backgroundColor: col.color }">
          {{ col.name }}
        </div>
        <div class="column-content">
          <div
            v-for="task in tasks.filter((t) => t.status === col.name)"
            :key="task.id"
            class="task-card"
            :style="{ borderLeftColor: col.color }"
          >
            {{ task.title }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.board-container {
  background-color: #fff1db;
  padding: 20px;
  border-radius: 12px;

  width: 100%;
  box-sizing: border-box;
  margin: 0 auto;
  font-family: sans-serif;
}

.board-title {
  color: #1e293b;
  text-align: center;
  margin-top: 0;
  margin-bottom: 20px;
}

.board-columns {
  display: flex;
  gap: 15px;
}

.column {
  flex: 1;
  background-color: #fffdf4;
  border-radius: 8px;
  overflow: hidden;
  min-height: 700px; /* Macht die Spalten lang nach unten */
  width: 1200px;
  display: flex;
  flex-direction: column;
}

.column-header {
  padding: 10px;
  text-align: center;
  font-weight: bold;
  color: #1e293b;
}

.column-content {
  padding: 10px;
  flex: 1;
}

.task-card {
  background-color: white;
  padding: 12px;
  border-radius: 6px;
  margin-bottom: 10px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  color: #334155;


  border-left: 7.5px solid #ccc;
}
</style>
