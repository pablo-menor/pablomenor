<script setup>
import { log } from 'node_modules/astro/dist/core/logger/core'
import { ref, onMounted } from 'vue'

// reactive state
const selectedTab = ref(0)

</script>

<template>
  <button @click="increment">Count is: ¡4</button>
  <h1>defe</h1>
</template>