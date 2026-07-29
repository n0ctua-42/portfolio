<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import logo1 from '../assets/logo 1.jpeg'

const menuOpen = ref(false)

const navRef = ref(null)
const underlineStyle = ref({ left: '0px', width: '0px' })
let sectionObserver = null

function toggleMenu() {
  menuOpen.value = !menuOpen.value
}

function closeMenu() {
  menuOpen.value = false
}

function moveIndicatorTo(el) {
  if (!el || !navRef.value) return
  const navRect = navRef.value.getBoundingClientRect()
  const elRect = el.getBoundingClientRect()
  // make underline slightly shorter than the text (60%) and center it
  const targetWidth = Math.max(14, Math.round(elRect.width * 0.6))
  const left = Math.round(elRect.left - navRect.left + (elRect.width - targetWidth) / 2)
  underlineStyle.value = { left: `${left}px`, width: `${targetWidth}px` }
}

function scrollToSection(id) {
  const section = document.getElementById(id)
  if (!section) return

  const navHeight = navRef.value?.getBoundingClientRect().height || 0
  const sectionRect = section.getBoundingClientRect()
  const viewportHeight = window.innerHeight
  const sectionHeight = sectionRect.height
  const sectionTop = window.scrollY + sectionRect.top
  const availableHeight = viewportHeight - navHeight

  let targetScroll = sectionTop - navHeight

  if (sectionHeight < availableHeight) {
    targetScroll = sectionTop - navHeight - (availableHeight - sectionHeight) / 2
  }

  const maxScroll = Math.max(0, document.documentElement.scrollHeight - viewportHeight)
  targetScroll = Math.min(Math.max(targetScroll, 0), maxScroll)

  window.scrollTo({ top: targetScroll, behavior: 'smooth' })
}

function onNavLinkClick(e) {
  e.preventDefault()
  const el = e.currentTarget
  // close mobile menu if open
  closeMenu()
  // update active class
  const links = navRef.value?.querySelectorAll('.nav-link') || []
  links.forEach((ln) => ln.classList.remove('active'))
  el.classList.add('active')

  const href = el.getAttribute('href')
  const targetId = href && href.startsWith('#') ? href.slice(1) : null
  if (targetId) {
    scrollToSection(targetId)
  }

  nextTick(() => moveIndicatorTo(el))
}

function handleResize() {
  // reposition under the currently centred underline target if possible
  const active = navRef.value?.querySelector('.nav-link.active') || navRef.value?.querySelector('a[href="#about"]') || navRef.value?.querySelector('.nav-link')
  if (active) moveIndicatorTo(active)
}

onMounted(() => {
  // position indicator on the "à propos" link by default
  nextTick(() => {
    const defaultLink = navRef.value?.querySelector('a[href="#about"]') || navRef.value?.querySelector('.nav-link')
    if (defaultLink) {
      // mark active for potential styling
      defaultLink.classList.add('active')
      moveIndicatorTo(defaultLink)
    }
  })
  window.addEventListener('resize', handleResize)
  // observe sections and move underline on section change
  const sections = Array.from(document.querySelectorAll('section[id]'))
  if (sections.length) {
    sectionObserver = new IntersectionObserver(
      (entries) => {
        const visible = entries.filter(e => e.isIntersecting).sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0]
        if (visible) {
          const id = visible.target.id
          const link = navRef.value?.querySelector(`a[href="#${id}"]`)
          if (link) {
            const links = navRef.value?.querySelectorAll('.nav-link') || []
            links.forEach((ln) => ln.classList.remove('active'))
            link.classList.add('active')
            moveIndicatorTo(link)
          }
        }
      },
      { threshold: [0.25, 0.5, 0.75] }
    )
    sections.forEach((s) => sectionObserver.observe(s))
  }
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
  if (sectionObserver) sectionObserver.disconnect()
})
</script>

<template>
  <header class="site-header">
    <div class="header-inner">
      <a href="#top" class="logo">
        <span class="logo-icon-wrapper">
          <img :src="logo1" alt="Logo" class="logo-icon" />
        </span>
        Tojo
      </a>

      <nav class="main-nav" ref="navRef" :class="{ open: menuOpen }">
        <a href="#about" class="nav-link" @click="onNavLinkClick">à propos</a>
        <a href="#skills" class="nav-link" @click="onNavLinkClick">compétences</a>
        <a href="#projects" class="nav-link" @click="onNavLinkClick">projets</a>
        <a href="#experience" class="nav-link" @click="onNavLinkClick">expérience</a>
        <a href="#education" class="nav-link" @click="onNavLinkClick">formation</a>
        <a href="#contact" class="nav-link" @click="onNavLinkClick">contact</a>
        <span class="nav-underline" :style="underlineStyle"></span>
      </nav>

      <button class="nav-toggle" @click="toggleMenu" :aria-expanded="menuOpen" aria-label="Ouvrir le menu">
        <span v-if="!menuOpen">☰</span>
        <span v-else>✕</span>
      </button>
    </div>
  </header>
</template>

<style scoped>
.site-header {
  position: sticky;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  z-index: 50;
  background: rgba(255, 255, 255, 0.90);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px); /* Safari */
  border-bottom: 1px solid rgba(0, 0, 0, 0.08);
}
.header-inner {
  max-width: 1120px;
  margin: 0 auto;
  padding: 0 24px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 20px;
  min-height: var(--nav-height);
}
.logo { 
  display: inline-flex;
  align-items: center;
  gap: 12px;
  font-family: var(--font-space); 
  font-weight: 600; 
  font-size: 18px; 
  color: var(--ink); 
  letter-spacing: -0.5px;
  text-decoration: none;
  transition: opacity 0.3s ease;
}

.logo-icon-wrapper {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.88);
  display: grid;
  place-items: center;
  box-shadow: 0 10px 24px rgba(0, 0, 0, 0.08);
}

.logo-icon {
  width: 35px;
  height: 35px;
  object-fit: cover;
  border-radius: 50%;
}
.logo:hover { opacity: 0.7; }
.main-nav { display: flex; flex-wrap: wrap; gap: 28px; margin-left: auto; position: relative; padding-bottom: 10px; max-width: 100%; }
.nav-link { font-family: var(--font-sans); font-size: 14px; color: var(--slate); position: relative; padding: 6px 2px; text-decoration: none; white-space: nowrap; }
.nav-link:hover { color: var(--teal); }
.nav-link.active { color: var(--ink); }

/* underline indicator */
.nav-underline {
  position: absolute;
  bottom: 2px;
  left: 0;
  height: 4px;
  width: 0;
  background: #000;
  border-radius: 3px;
  transition: left 360ms cubic-bezier(.2,.9,.3,1), width 360ms cubic-bezier(.2,.9,.3,1);
  pointer-events: none;
  will-change: left, width;
}

.nav-toggle {
  display: none;
  margin-left: auto;
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
  color: var(--ink);
}

@media (max-width: 860px) {
  .header-inner {
    padding: 0 18px;
    justify-content: space-between;
  }

  .main-nav {
    display: none;
    position: absolute;
    top: var(--nav-height);
    left: 0;
    right: 0;
    background: var(--bg);
    border-bottom: 1px solid var(--border);
    flex-direction: column;
    gap: 0;
    padding: 10px 18px 18px;
    width: 100%;
    z-index: 60;
  }

  .main-nav .nav-underline { display: none; }
  .main-nav.open { display: flex; }
  .main-nav .nav-link { padding: 14px 0; border-bottom: 1px solid var(--border); font-size: 15px; }
  .nav-toggle { display: block; padding: 10px; }
}
</style>