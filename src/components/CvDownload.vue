<template>
  <div class="cv-download" ref="rootRef">
    <button
      type="button"
      class="toggle-btn"
      :class="{ 'is-open': menuOpen }"
      @click="toggleMenu"
      :aria-expanded="menuOpen.toString()"
      aria-haspopup="menu"
    >
      Télécharger mon CV
      <ChevronDown class="chevron" aria-hidden="true" :size="18" :stroke-width="2" />
    </button>

    <Transition name="dropdown">
      <div v-if="menuOpen" class="dropdown-menu" role="menu">
        <a
          class="dropdown-item"
          :href="pdfDev"
          download=" CV_DEV_ANDRIMANDIMBISON_TOJO"
          role="menuitem"
          @click="closeMenu"
        >
          CV Développeur
        </a>
        <a
          class="dropdown-item dropdown-item--separator"
          :href="pdfReseau"
          download="CV_RÉSEAUX_ANDRIMANDIMBISON TOJO"
          role="menuitem"
          @click="closeMenu"
        >
          CV Réseau & Support IT
        </a>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { ChevronDown } from 'lucide-vue-next'

// PDF importés via Vite 
const pdfDev = new URL('../assets/cv/cv-dev.pdf', import.meta.url).href
const pdfReseau = new URL('../assets/cv/cv-reseau.pdf', import.meta.url).href

const menuOpen = ref(false)
const rootRef = ref(null)

function toggleMenu() {
  menuOpen.value = !menuOpen.value
}

function closeMenu() {
  menuOpen.value = false
}

// Ferme le menu si le clic est en dehors du composant
function onClickOutside(event) {
  if (rootRef.value && !rootRef.value.contains(event.target)) {
    closeMenu()
  }
}

// Ferme le menu avec Échap
function onKeydown(event) {
  if (event.key === 'Escape') {
    closeMenu()
  }
}

onMounted(() => {
  document.addEventListener('click', onClickOutside)
  document.addEventListener('keydown', onKeydown)
})

onUnmounted(() => {
  document.removeEventListener('click', onClickOutside)
  document.removeEventListener('keydown', onKeydown)
})
</script>

<style scoped>
.cv-download {
  position: relative;
  display: inline-block;
  font-family: inherit;
  margin-top: clamp(16px, 3vw, 25px);
}

.toggle-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.95rem 1.3rem;
  border: none;
  border-radius: 12px;
  background: #111111;
  color: #ffffff;
  font-weight: 700;
  cursor: pointer;
  transition: transform .28s, box-shadow .28s, background .28s;
  box-shadow: 0 6px 18px rgba(17, 17, 17, 0.08);
}

.toggle-btn:hover,
.toggle-btn:focus {
  transform: translateY(-4px);
  box-shadow: 0 18px 44px rgba(17, 17, 17, 0.12);
}

.chevron {
  transition: transform .2s ease;
}

.toggle-btn.is-open .chevron {
  transform: rotate(180deg);
}

.dropdown-menu {
  position: absolute;
  top: calc(100% + 0.75rem);
  left: 0;
  min-width: 220px;
  max-width: 100%;
  background: #ffffff;
  border-radius: 16px;
  border: 1px solid rgba(16, 36, 47, 0.08);
  box-shadow: 0 18px 44px rgba(2, 6, 23, 0.08);
  overflow: hidden;
  z-index: 10;
}

.dropdown-item {
  display: block;
  width: 100%;
  padding: 0.95rem 1rem;
  color: #10242f;
  text-decoration: none;
  background: #ffffff;
  transition: background .28s, color .28s;
}

.dropdown-item:hover,
.dropdown-item:focus {
  background: #111111;
  color: #ffffff;
}

.dropdown-item--separator {
  border-top: 1px solid #e6ebe8;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

.dropdown-enter-active,
.dropdown-leave-active {
  transition: opacity 200ms ease, transform 200ms ease;
}

@media (max-width: 640px) {
  .dropdown-menu {
    position: relative;
    top: auto;
    left: auto;
  }
}
</style>
