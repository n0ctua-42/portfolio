<script setup>
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
</script>

<template>
  <section class="section" id="projects">
    <p class="section-eyebrow">projets</p>
    <h2 class="section-title">Projets réalisés</h2>

    <div class="project-grid">
      <article class="project-card" v-for="project in projects" :key="project.title">
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
.section { padding: 88px 24px; max-width: 1120px; margin: 0 auto; }
.section-eyebrow { font-family: var(--font-mono); font-size: 13px; color: var(--copper); margin-bottom: 12px; }
.section-title { font-size: 28px; max-width: 640px; margin-bottom: 44px; }
.project-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 24px; }
.project-card { background: var(--surface); border: 1px solid var(--border); border-radius: 16px; padding: 28px; }
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
.project-badge--net { background: #FBF0DF; color: var(--copper-dark); }
.project-card h3 { font-size: 18px; margin-bottom: 6px; }
.project-stack { font-family: var(--font-mono); font-size: 12.5px; color: var(--slate); margin-bottom: 16px; }
.project-card ul { display: flex; flex-direction: column; gap: 8px; padding-left: 16px; }
.project-card li { font-size: 14px; color: var(--slate); }
</style>