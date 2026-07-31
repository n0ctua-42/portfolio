<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const progress = ref(0)

const handleScroll = () => {
  const scrollTop = window.scrollY
  const docHeight = document.documentElement.scrollHeight - window.innerHeight
  const scrolled = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0
  progress.value = scrolled
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div class="progress-container">
    <div class="progress-bar" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<style scoped>
.progress-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: rgba(255, 255, 255, 0.1);
  z-index: 1000;
  backdrop-filter: blur(1px);
}

.progress-bar {
  position:relative;
  height: 100%;
  background: var(--ink);
  box-shadow: 0 0 6px rgba(16, 36, 47, 0.3);
  width: 0%;
  transition: width 0.1s ease-out;
  border-radius: 0 1px 1px 0;
}

.progress-bar::after {
  content: '';
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 6px;
  height: 8px;
  background: var(--ink);
  border-radius: 1px;
  box-shadow: 0 0 4px rgba(16, 36, 47, 0.4);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% {
    box-shadow: 0 0 4px rgba(16, 36, 47, 0.3);
  }
  50% {
    box-shadow: 0 0 8px rgba(16, 36, 47, 0.5);
  }
}
</style>
