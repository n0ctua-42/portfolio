<script setup>
import { Github, Linkedin, ArrowUp } from 'lucide-vue-next'
import { Icon } from '@iconify/vue'

const year = new Date().getFullYear()
function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer class="site-footer" role="contentinfo">
    <div class="footer-inner">
      <p class="footer-tagline">Développeur Full Stack • Réseaux • Cybersécurité</p>

      <nav class="footer-social" aria-label="Réseaux sociaux">
        <a class="social-link" href="https://github.com/n0ctua-42" target="_blank" rel="noopener noreferrer" aria-label="GitHub">
          <Github :size="20" :stroke-width="2" aria-hidden="true" />
        </a>

        <!-- Profil LinkedIn -->
        <a class="social-link" href="https://www.linkedin.com/in/tojo-andriamandimbison-9879113b1/?isSelfProfile=true" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn">
          <Linkedin :size="20" :stroke-width="2" aria-hidden="true" />
        </a>

        <!--Profil Discord -->
        <a class="social-link" href="https://discord.com/users/1292926460352397388" target="_blank" rel="noopener noreferrer" aria-label="Discord">
          <Icon icon="simple-icons:discord" width="20" aria-hidden="true" />
        </a>
      </nav>

      <hr class="footer-sep" />

      <div class="footer-bottom">
        <p class="copyright">© {{ year }} ANDRIAMANDIMBISON Tojo Santatriniaina. Tous droits réservés.</p>
        <button class="back-top" @click="scrollToTop" aria-label="Retour en haut">
          <ArrowUp :size="16" :stroke-width="2" class="back-top-icon" aria-hidden="true" />
          Retour en haut
        </button>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  background: #0f172a;
  color: rgba(255,255,255,0.95);
  border-top: 1px solid rgba(255,255,255,0.04);
  padding: 48px 20px;
}
.footer-inner {
  max-width: 1120px;
  margin: 0 auto;
  background: transparent;
  border-radius: 12px 12px 0 0;
  padding: 18px 20px 0 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.footer-tagline {
  font-family: var(--font-sans);
  font-size: 15px;
  color: rgba(255,255,255,0.9);
  letter-spacing: 0.02em;
  margin: 0;
}
.footer-social {
  display: flex;
  gap: 14px;
  align-items: center;
}
.social-link {
  display: inline-grid;
  place-items: center;
  width: 44px;
  height: 44px;
  background: rgba(255,255,255,0.03);
  color: rgba(255,255,255,0.9);
  border-radius: 10px;
  transition: transform 0.28s cubic-bezier(.2,.9,.3,1), background 0.28s, box-shadow 0.28s;
  text-decoration: none;
}
.social-link svg { width: 20px; height: 20px; }
.social-link:hover, .social-link:focus {
  transform: translateY(-4px);
  background: rgba(255,255,255,0.08);
  box-shadow: 0 10px 30px rgba(2,6,23,0.5);
  color: #ffffff;
}
.footer-sep {
  border: 0;
  height: 1px;
  background: linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.04), rgba(255,255,255,0.02));
  margin: 6px 0 4px 0;
}
.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 12px 0 10px 0;
}
.copyright {
  font-family: var(--font-sans);
  font-size: 13px;
  color: rgba(255,255,255,0.8);
  margin: 0;
}
.back-top {
  font-family: var(--font-sans);
  background: transparent;
  color: rgba(255,255,255,0.95);
  border: 1px solid rgba(255,255,255,0.08);
  padding: 10px 14px;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.28s cubic-bezier(.2,.9,.3,1), box-shadow 0.28s, background 0.28s;
  display: inline-flex;
  align-items: center;
}
.back-top-icon {
  margin-right: 8px;
  display: inline-flex;
}
.back-top:hover, .back-top:focus {
  transform: translateY(-4px);
  background: rgba(255,255,255,0.06);
  box-shadow: 0 14px 34px rgba(2,6,23,0.5);
}

/* small screen adjustments */
@media (max-width: 860px) {
  .footer-inner { padding: 12px 14px 0 14px; }
  .footer-bottom { flex-direction: column; align-items: flex-start; gap: 10px; }
  .back-top { align-self: stretch; text-align: center; }
}

@media (max-width: 560px) {
  .footer-inner { padding: 14px 16px 0 16px; }
  .footer-social { flex-wrap: wrap; justify-content: center; }
  .footer-bottom { align-items: center; text-align: center; }
  .back-top { width: 100%; }
}

/* legacy fallback button style (kept from previous template) */
.btn-link { background: none; border: none; cursor: pointer; font-family: var(--font-mono); font-size: 13px; color: var(--slate); }
.btn-link:hover { color: var(--teal); }

</style>