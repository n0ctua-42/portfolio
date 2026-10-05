<script setup>
import { ref, onMounted } from 'vue'

const projects = [
  {
    type: 'dev',
    title: 'Trello',
    stack: 'NestJS · TypeScript · PostgreSQL · Sequelize · JWT · REST API',
    points: [
      "API backend d'une application collaborative de gestion de projets inspirée de Trello.",
      "Architecture modulaire avec gestion des utilisateurs, projets, tableaux, listes, tâches, labels, commentaires et checklists.",
      "Authentification JWT et sécurisation des routes avec guards et contrôle des accès.",
      "Persistance des données avec Sequelize et PostgreSQL, avec gestion de relations entre les différentes entités.",
      "Validation des données avec DTO et class-validator, gestion centralisée des erreurs et structuration propre du backend.",
      "Développement d'une API REST destinée à être consommée par un frontend Vue.js.",
    ]
  },
  {
    type: 'dev',
    title: "WebSocket Real-Time",
    stack: 'NestJS · TypeScript · WebSocket · REST API',
    points: [
      "Application temps réel développée avec NestJS pour expérimenter la communication bidirectionnelle via WebSocket.",
      "Mise en place d'un système de rooms permettant à plusieurs clients de rejoindre un même espace de communication.",
      "Transmission et diffusion instantanée des messages entre les clients connectés.",
      "Utilisation des WebSocket Gateway de NestJS pour gérer les connexions, événements et communications temps réel.",
      "Projet réalisé pour approfondir l'intégration du temps réel dans une architecture backend NestJS.",
    ]
  },
  {
    type: 'dev',
    title: "API Auth Prisma JWT",
    stack: 'Node.js · TypeScript · Express · Prisma · PostgreSQL · JWT',
    points: [
      "API REST sécurisée développée avec Node.js et Express pour la gestion des utilisateurs.",
      "Authentification basée sur JWT avec gestion des rôles admin et user.",
      "Utilisation de Prisma ORM pour communiquer avec une base de données PostgreSQL.",
      "Hachage sécurisé des mots de passe et protection des ressources nécessitant une authentification.",
      "Mise en place d'un système de contrôle d'accès basé sur les rôles (RBAC).",
      "Projet permettant d'expérimenter Prisma et PostgreSQL dans une architecture d'API REST.",
    ]
  },
  {
    type: 'dev',
    title: "Todo App API",
    stack: 'NestJS · TypeScript · Sequelize · MySQL · JWT · Swagger',
    points: [
      "API REST de gestion de tâches construite avec NestJS selon une architecture modulaire.",
      "Authentification et sécurisation des routes avec JWT et Passport.",
      "Gestion complète des utilisateurs et des tâches avec opérations CRUD.",
      "Persistance des données avec Sequelize et MySQL, avec relations entre les entités.",
      "Validation des requêtes avec class-validator et gestion centralisée des erreurs HTTP.",
      "Documentation interactive de l'API avec Swagger.",
      "Mise en place de guards et d'une architecture séparant controllers, services, modules et accès aux données.",
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