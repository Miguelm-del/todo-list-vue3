<template>
  <div class="app">
    <h1>Minha Lista de Tarefas</h1>
    <input v-model="newTaskText" placeholder="Digite uma tarefa" @keyup.enter="addTask" />
    <button @click="addTask">Adicionar</button>

    <div class="labels">
      <p class="pending-count">Pendentes: {{ pendingCount }}</p>
      <p class="done-count">Concluidas: {{ doneCount }}</p>
    </div>

    <TaskList
      :tasks="tasks"
      @toggle-complete="toggleComplete"
      @edit-task="editTask"
      @remove-task="removeTask"
    />
  </div>
</template>

<script setup>
import TaskList from '@/components/TaskList.vue'
import { ref, computed } from 'vue'

const tasks = ref([])
const newTaskText = ref('')

function addTask() {
  if (newTaskText.value.trim() !== '') {
    tasks.value.push({
      id: Date.now(),
      text: newTaskText.value,
      completed: false,
    })
    newTaskText.value = ''
  }
}

function toggleComplete(taskId) {
  const task = tasks.value.find((t) => t.id === taskId)
  if (task) {
    task.completed = !task.completed
  }
}

function editTask({ id, newText }) {
  const task = tasks.value.find((t) => t.id === id)
  if (task) {
    task.text = newText
  }
}

function removeTask(id) {
  tasks.value = tasks.value.filter((t) => t.id !== id)
}

const pendingCount = computed(() => tasks.value.filter((t) => !t.completed).length)

const doneCount = computed(() => tasks.value.filter((t) => t.completed).length)
</script>

<style>
.app {
  max-width: 400px;
  margin: auto;
  font-family: sans-serif;
}

input {
  width: 70%;
  padding: 10px;
}

button {
  padding: 10px 10px;
  margin-left: 5px;
}

.labels {
  display: flex;
  gap: 32px;
}

.done-count {
  color: #59b877;
  font-weight: 600;
}

.pending-count {
  color: rgb(255, 166, 0);
  font-weight: 600;
}
</style>
