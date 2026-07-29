<script setup>
import { ref, onMounted } from 'vue'

const projects = [
  {
    type: 'dev',
    title: 'SmartTodo',
    stack: 'NestJS · JWT · Sequelize · MySQL · Swagger',
    points: [
      "API de gestion de tâches construite avec NestJS, architecture modulaire.",
      "Authentification et sécurisation des routes avec JWT.",
      "Persistance des données via Sequelize sur MySQL, avec relations et migrations.",
      "Documentation interactive de l'API avec Swagger."
    ]
  },
  {
    type: 'dev',
    title: "Application d'authentification sécurisée",
    stack: 'Node.js · Express · Prisma · PostgreSQL · JWT',
    points: [
      "Développement d'une API REST sécurisée avec Prisma ORM et PostgreSQL.",
      "Authentification basée sur JWT, chiffrement des mots de passe avec bcrypt."
    ]
  },
  {
    type: 'net',
    title: 'Projet réseau — stage pratique',
    stack: 'LAN · TCP/IP · Configuration & maintenance',
    points: [
      "Configuration et maintenance d'un réseau local appliqué à des situations réelles en entreprise."
    ]
  },
  {
    type: 'net',
    title: 'Projet de sécurité réseau',
    stack: 'Protocoles de sécurité · Réduction des vulnérabilités',
    points: [
      "Mise en place d'un protocole de sécurité réseau visant à réduire les vulnérabilités."
    ]
  }
]

const sectionRef = ref(null)
const sectionVisible = ref(false)

onMounted(() => {
  const sectionObserver = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        sectionVisible.value = true
        sectionObserver.disconnect()
      }
    },
    { threshold: 0.2 }
  )

  if (sectionRef.value) sectionObserver.observe(sectionRef.value)
})
</script>

<template>
  <section ref="sectionRef" :class="['section', { 'section--visible': sectionVisible }]" id="projects">
    <p class="section-eyebrow">projets</p>
    <h2 class="section-title">Projets réalisés</h2>

    <div class="project-grid">
      <article
        class="project-card"
        v-for="project in projects"
        :key="project.title"
        :class="{ 'project-card--visible': sectionVisible }"
      >
        <span class="project-badge" :class="project.type === 'net' ? 'project-badge--net' : ''">
          {{ project.type === 'net' ? 'réseau' : 'développement' }}
        </span>
        <h3>{{ project.title }}</h3>
        <p class="project-stack">{{ project.stack }}</p>
        <ul>
          <li v-for="point in project.points" :key="point">{{ point }}</li>
        </ul>
      </article>
    </div>
  </section>
</template>

<style scoped>
.section {
  padding: clamp(3rem, 5vw, 4rem) 1.5rem;
  max-width: min(1120px, 100%);
  margin: 0 auto;
  min-height: auto;
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.9s ease, transform 0.9s ease;
  scroll-margin-top: calc(var(--nav-height) + 20px);
}
.section--visible {
  opacity: 1;
  transform: translateY(0);
}
.section-eyebrow {
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--copper);
  margin-bottom: 12px;
}
.section-title {
  font-size: 28px;
  max-width: 640px;
  margin-bottom: 44px;
}
.project-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 24px;
}
.project-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: clamp(22px, 2vw, 28px);
  box-shadow: 0 16px 34px rgba(17, 17, 17, 0.12);
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.8s ease, transform 0.8s ease, box-shadow 0.25s ease;
}
.project-card--visible {
  opacity: 1;
  transform: translateY(0);
}
.project-badge {
  display: inline-block;
  font-family: var(--font-mono);
  font-size: 11px;
  text-transform: uppercase;
  padding: 4px 10px;
  border-radius: 12px;
  background: var(--teal-tint);
  color: var(--teal-dark);
  margin-bottom: 14px;
}
.project-badge--net {
  background: #FBF0DF;
  color: var(--copper-dark);
}
.project-card h3 {
  font-size: 18px;
  margin-bottom: 6px;
}
.project-stack {
  font-family: var(--font-mono);
  font-size: 12.5px;
  color: var(--slate);
  margin-bottom: 16px;
}
.project-card ul {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding-left: 16px;
}
.project-card li {
  font-size: 14px;
  color: var(--slate);
}
@media (max-width: 900px) {
  .section {
    padding: 64px 18px;
  }

  .section-title {
    font-size: 26px;
    margin-bottom: 36px;
  }

  .project-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

@media (max-width: 600px) {
  .section {
    padding: 52px 14px;
  }

  .project-card {
    padding: 20px;
  }
}
</style>