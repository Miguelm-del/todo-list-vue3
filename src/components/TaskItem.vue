<template>
  <li
    :style="{ textDecoration: task.completed ? 'line-through' : 'none' }"
    @click="toggle"
    class="task-item"
  >
    {{ task.text }}
  </li>
</template>

<script setup>
const props = defineProps({
  task: Object,
  required: true,
})

const emit = defineEmits(['toggle'])

function toggle() {
  emit('toggle', props.task?.id)
}
</script>

<style>
.task-item {
  cursor: pointer;
  margin: 5px 0;
  color: black;
  font-weight: bolder;
}
</style>
