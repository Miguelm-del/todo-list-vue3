<template>
  <ul>
    <TaskItem v-for="task in tasks" :key="task.id" :task="task" @toggle="handleToggle" />
  </ul>
</template>

<script setup>
import TaskItem from './TaskItem.vue'

const props = defineProps({
  tasks: Array,
})
const emit = defineEmits(['toggle-complete'])

function handleToggle(taskId) {
  emit('toggle-complete', taskId)
}
</script>
