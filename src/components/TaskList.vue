<template>
  <ul>
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @toggle="handleToggle"
      @edit="handleEdit"
      @remove="handleRemove"
    />
  </ul>
</template>

<script setup>
import TaskItem from './TaskItem.vue'

const props = defineProps({
  tasks: Array,
})
const emit = defineEmits(['toggle-complete', 'edit-task', 'remove-task'])

function handleToggle(taskId) {
  emit('toggle-complete', taskId)
}

function handleEdit(payload) {
  emit('edit-task', payload)
}

function handleRemove(id) {
  emit('remove-task', id)
}
</script>
