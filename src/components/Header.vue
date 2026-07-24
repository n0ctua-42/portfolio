<template>
  <header class="site-header">
    <div class="header-inner">
      <a href="#top" class="logo">ATS<span class="logo-dot">.</span></a>

      <nav class="main-nav">
        <a href="#about" class="nav-link">à propos</a>
        <a href="#skills" class="nav-link">compétences</a>
        <a href="#projects" class="nav-link">projets</a>
        <a href="#experience" class="nav-link">expérience</a>
        <a href="#education" class="nav-link">formation</a>
        <a href="#contact" class="nav-link">contact</a>
      </nav>

    </div>
  </header>
</template>

<style scoped>
.site-header {
  position: sticky;
  top: 0;
  z-index: 50;
  background: rgba(241, 244, 243, 0.92);
  border-bottom: 1px solid var(--border);
}
.header-inner {
  max-width: 1120px;
  margin: 0 auto;
  padding: 0 24px;
  display: flex;
  align-items: center;
  gap: 24px;
  height: 68px;
}
.logo { font-family: var(--font-mono); font-weight: 500; font-size: 18px; color: var(--ink); }
.logo-dot { color: var(--copper); }
.main-nav { display: flex; gap: 28px; margin-left: auto; }
.nav-link { font-family: var(--font-mono); font-size: 14px; color: var(--slate); }
.nav-link:hover { color: var(--teal); }
</style>