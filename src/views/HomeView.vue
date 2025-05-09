<template>
  <div>
    <h1>{{ text }}</h1>

    <input v-model="text" placeholder="Digite o titulo da página" />
  </div>
</template>

<script setup>
import { ref } from 'vue'

const text = ref('Hello World!')
</script>
