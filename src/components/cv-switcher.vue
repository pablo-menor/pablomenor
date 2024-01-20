<script setup>
import { log } from 'node_modules/astro/dist/core/logger/core'
import { ref, onMounted } from 'vue'

// reactive state
const selectedTab = ref(0)

const increment = () => {
  confetti({
  particleCount: 700,
  spread: 500,
  origin: { y: 0.6 },
});
}

// lifecycle hooks
onMounted(() => {
  const script = document.createElement("script");
    script.src = "https://cdn.jsdelivr.net/npm/@tsparticles/confetti@3.0.3/tsparticles.confetti.bundle.min.js";
    script.async = true;
    document.head.appendChild(script);

})
</script>

<template>
  <button @click="increment">Count is: ¡4</button>
  <h1>defe</h1>
</template>