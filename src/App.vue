<script setup>
// 1. LA LOGIQUE — les données, les fonctions
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <!-- 2. LA STRUCTURE — ce qui s'affiche, un HTML "augmenté" -->
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
/* 3. LE STYLE — le CSS, isolé à ce fichier seulement */
.logo { height: 6em; }
</style>