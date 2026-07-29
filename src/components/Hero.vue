<script setup>
import profileImg from '../assets/profile.png'
import CvDownload from './CvDownload.vue'
</script>

<template>
  <section id="about" class="hero">
    <div class="hero-inner">
      <div class="hero-text">
        <p class="eyebrow">développeur full stack junior · réseaux &amp; télécom</p>
        <h1 class="hero-title">Andriamandimbison<br>Tojo Santatriniaina</h1>
        <p class="hero-lede">
          Je conçois des applications web robustes avec Node.js et NestJS, et je m'appuie
          sur une base solide en réseaux et infrastructures pour construire des systèmes
          qui tiennent la route de bout en bout.
        </p>
        <CvDownload />
      </div>

      <div class="profile-container">
        <div class="profile-frame">
          <img :src="profileImg" alt="Andriamandimbison Tojo" class="profile-image">
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero { 
  padding: clamp(3rem, 6vw, 5rem) 1.5rem;
  font-family: var(--font-space);
  min-height: auto;
}

.hero-inner {
  max-width: min(1120px, 100%);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.15fr 0.85fr;
  gap: clamp(32px, 5vw, 56px);
  align-items: center;
}

.eyebrow { 
  font-family: var(--font-mono); 
  font-size: 13px; 
  color: var(--teal); 
  margin-bottom: 18px;
  letter-spacing: 0.02em;
}

.hero-title { 
  font-size: 44px; 
  line-height: 1.15; 
  margin-bottom: 20px;
  color: var(--ink);
  font-weight: 600;
  font-family: var(--font-space);
}

.hero-lede { 
  font-size: 17px; 
  color: var(--slate); 
  max-width: 480px;
  line-height: 1.7;
}

.profile-container {
  display: flex;
  justify-content: center;
  align-items: center;
  animation: fadeInUp 0.8s ease-out 0.2s both;
}

.profile-frame {
  position: relative;
  width: 100%;
  max-width: 380px;
  aspect-ratio: 1;
  border-radius: 20px;
  overflow: hidden;
  background: linear-gradient(135deg, var(--teal-tint) 0%, rgba(255, 255, 255, 0.5) 100%);
  border: 1px solid rgba(201, 138, 46, 0.15);
  box-shadow: 0 20px 60px rgba(16, 36, 47, 0.12),
              0 0 40px rgba(33, 91, 87, 0.08);
  transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
}

.profile-frame::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(201, 138, 46, 0) 0%, rgba(33, 91, 87, 0.05) 100%);
  pointer-events: none;
  z-index: 2;
}

.profile-frame:hover {
  box-shadow: 0 24px 72px rgba(16, 36, 47, 0.18),
              0 0 48px rgba(33, 91, 87, 0.12);
  transform: translateY(-8px);
}

.profile-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

.profile-frame:hover .profile-image {
  transform: scale(1.03);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 1024px) {
  .hero-inner {
    gap: 40px;
  }

  .hero-title {
    font-size: 38px;
  }

  .profile-frame {
    max-width: 320px;
  }
}

@media (max-width: 860px) {
  .hero {
    padding: 64px 24px;
  }

  .hero-inner {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .hero-title {
    font-size: 32px;
    line-height: 1.2;
  }

  .hero-lede {
    font-size: 16px;
  }

  .profile-frame {
    max-width: 100%;
    margin: 0 auto;
  }
}

@media (max-width: 640px) {
  .hero {
    padding: 48px 16px;
  }

  .hero-inner {
    gap: 32px;
  }

  .hero-title {
    font-size: 28px;
    margin-bottom: 16px;
  }

  .hero-lede {
    font-size: 15px;
  }

  .eyebrow {
    font-size: 12px;
  }

  .profile-frame {
    max-width: 100%;
    border-radius: 16px;
  }
}

@media (max-width: 480px) {
  .hero {
    padding: 40px 12px;
  }

  .hero-inner {
    gap: 24px;
  }

  .hero-title {
    font-size: 24px;
    line-height: 1.25;
    margin-bottom: 12px;
  }

  .hero-lede {
    font-size: 14px;
    max-width: 100%;
  }
}
</style>