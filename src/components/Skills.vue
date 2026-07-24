<script setup>
const devSkills = [
  { title: 'Front-end', tags: ['HTML5', 'CSS3', 'JavaScript (ES6+)', 'Vue.js', 'Vue Router', 'Vuex / Pinia', 'Jest', 'Vitest'] },
  { title: 'Back-end', tags: ['Node.js', 'Express', 'NestJS', 'TypeScript', 'JWT', 'bcrypt', 'Swagger'] },
  { title: 'Bases de données', tags: ['PostgreSQL', 'MySQL', 'Prisma ORM', 'Sequelize'] },
  { title: 'Outils & workflow', tags: ['Git', 'Gitflow', 'Docker'] }
]

const netSkills = [
  { title: 'Systèmes', tags: ['Windows 10 / 11', 'Linux (bases)'] },
  { title: 'Réseaux', tags: ['LAN', 'TCP/IP', 'VPN', 'DHCP', 'DNS', 'Diagnostic réseau'] },
  { title: 'Support IT', tags: ['Support N1/N2', 'Sécurisation de postes', 'Dépannage matériel'] },
  { title: 'Outils', tags: ['GLPI', 'Documentation technique'] }
]
</script>

<template>
  <section class="section" id="skills">
    <p class="section-eyebrow">compétences</p>
    <h2 class="section-title">Deux terrains, un seul niveau d'exigence</h2>

    <div class="skills-columns">
      <div class="skill-block skill-block--dev">
        <h3>Développement</h3>
        <div class="skill-group" v-for="group in devSkills" :key="group.title">
          <h4>{{ group.title }}</h4>
          <div class="tag-row">
            <span class="tag" v-for="tag in group.tags" :key="tag">{{ tag }}</span>
          </div>
        </div>
      </div>

      <div class="skill-block skill-block--net">
        <h3>Réseaux &amp; support IT</h3>
        <div class="skill-group" v-for="group in netSkills" :key="group.title">
          <h4>{{ group.title }}</h4>
          <div class="tag-row">
            <span class="tag" v-for="tag in group.tags" :key="tag">{{ tag }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section { padding: 88px 24px; max-width: 1120px; margin: 0 auto; }
.section-eyebrow { font-family: var(--font-mono); font-size: 13px; color: var(--copper); margin-bottom: 12px; }
.section-title { font-size: 28px; max-width: 640px; margin-bottom: 44px; }
.skills-columns { display: grid; grid-template-columns: 1fr 1fr; gap: 28px; }
.skill-block {
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--teal);
  border-radius: 16px;
  padding: 32px;
}
.skill-block--net { border-left-color: var(--copper); }
.skill-block h3 { font-size: 20px; margin-bottom: 24px; }
.skill-group { margin-bottom: 20px; }
.skill-group h4 { font-size: 12.5px; color: var(--slate); text-transform: uppercase; margin-bottom: 10px; }
.tag-row { display: flex; flex-wrap: wrap; gap: 8px; }
.tag {
  font-size: 12.5px;
  font-family: var(--font-mono);
  padding: 5px 11px;
  border-radius: 6px;
  background: var(--teal-tint);
  color: var(--teal-dark);
}
.skill-block--net .tag { background: #FBF0DF; color: var(--copper-dark); }
</style>