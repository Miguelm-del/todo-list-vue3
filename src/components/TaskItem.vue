<template>
  <li
    :style="{ textDecoration: task.completed ? 'line-through' : 'none' }"
    :class="{ 'task-completed': task.completed }"
    @click="toggle"
    class="task-item"
  >
    {{ task.text }}

    <button class="button-task" @click.stop="edit">✏️</button>
    <button class="button-task" @click.stop="remove">🗑️</button>
  </li>
</template>

<script setup>
const props = defineProps({
  task: Object,
  required: true,
})

const emit = defineEmits(['toggle', 'edit', 'remove'])

function toggle() {
  emit('toggle', props.task?.id)
}

function edit() {
  const newText = prompt('Editar tarefa:', props.task.text)
  if (newText !== null && newText.trim() !== '') {
    emit('edit', { id: props.task.id, newText: newText.trim() })
  }
}

function remove() {
  emit('remove', props.task.id)
}
</script>

<style>
.task-item {
  cursor: pointer;
  margin: 5px 0;
  color: black;
  font-weight: bolder;
}

.button-task {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

.task-completed {
  color: hsla(160, 100%, 37%, 1);
  font-weight: bolder;
}
</style>
