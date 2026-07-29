<script setup>
import { ref, onMounted } from 'vue'
import { Icon } from '@iconify/vue'

const devSkills = [
  {
    title: 'Front-end',
    tags: [
      { name: 'HTML5', level: 82 },
      { name: 'CSS3', level: 80 },
      { name: 'JavaScript (ES6+)', level: 76 },
      { name: 'Vue.js', level: 75 },
      { name: 'Vue Router', level: 68 },
      { name: 'Vuex / Pinia', level: 70 },
      { name: 'Jest', level: 62 },
      { name: 'Vitest', level: 60 }
    ]
  },
  {
    title: 'Back-end',
    tags: [
      { name: 'Node.js', level: 70 },
      { name: 'Express', level: 68 },
      { name: 'NestJS', level: 64 },
      { name: 'TypeScript', level: 66 },
      { name: 'JWT', level: 62 },
      { name: 'bcrypt', level: 60 },
      { name: 'Swagger', level: 58 }
    ]
  },
  {
    title: 'Bases de données',
    tags: [
      { name: 'PostgreSQL', level: 68 },
      { name: 'MySQL', level: 66 },
      { name: 'Prisma ORM', level: 62 },
      { name: 'Sequelize', level: 60 }
    ]
  },
  {
    title: 'Outils & workflow',
    tags: [
      { name: 'Git', level: 72 },
      { name: 'Gitflow', level: 68 },
      { name: 'Docker', level: 66 }
    ]
  }
]

const netSkills = [
  {
    title: 'Systèmes',
    tags: [
      {
        name: 'Windows 10 / 11',
        description: 'Support utilisateur, configuration système, dépannage courant',
        level: 74
      },
      {
        name: 'Linux (Debian)',
        description: 'Administration de base, ligne de commande, gestion des services',
        level: 70
      }
    ]
  },
  {
    title: 'Réseaux',
    tags: [
      { name: 'LAN', description: 'Configuration et diagnostic réseau', level: 76 },
      { name: 'TCP/IP', description: 'Bonne compréhension des protocoles réseau', level: 74 },
      { name: 'DHCP / DNS', description: 'Configuration et résolution de problèmes', level: 70 },
      { name: 'VPN', description: 'Notions de fonctionnement et configuration', level: 68 },
      { name: 'Diagnostic réseau', description: 'Analyse des incidents avec ping, traceroute, etc.', level: 72 }
    ]
  },
  {
    title: 'Support IT',
    tags: [
      {
        name: 'Support N1/N2',
        description: 'Assistance utilisateur, résolution d’incidents logiciels et matériels',
        level: 74
      },
      {
        name: 'Sécurisation des postes',
        description: 'Bonnes pratiques de sécurité, mises à jour, gestion des accès',
        level: 72
      },
      {
        name: 'Dépannage matériel',
        description: 'Diagnostic des problèmes matériels courants',
        level: 70
      },
      {
        name: 'Documentation technique',
        description: 'Rédaction de procédures et rapports techniques',
        level: 68
      }
    ]
  },
  {
    title: 'Outils',
    tags: [
      { name: 'GLPI', description: 'Notions de gestion de parc et tickets', level: 64 },
      { name: 'Git/GitHub', description: 'Gestion de versions et collaboration technique', level: 72 }
    ]
  },
  {
    title: 'Cybersécurité',
    tags: [
      {
        name: 'Sécurité réseau',
        description: 'Défense réseau et segmentation',
        level: 78
      },
      {
        name: 'Sécurité des systèmes Linux',
        description: 'Renforcement Linux et gestion des permissions',
        level: 72
      },
      {
        name: 'Sécurité des applications Web (OWASP, JWT, bcrypt)',
        description: 'Protection web avec bonnes pratiques',
        level: 76
      }
    ]
  }
]

const techIcons = {
  'HTML5': 'simple-icons:html5',
  'CSS3': 'simple-icons:css3',
  'JavaScript (ES6+)': 'simple-icons:javascript',
  'Vue.js': 'simple-icons:vuedotjs',
  'Vue Router': 'simple-icons:vuedotjs',
  'Vuex / Pinia': 'simple-icons:pinia',
  'Node.js': 'simple-icons:nodedotjs',
  'Express': 'simple-icons:express',
  'NestJS': 'simple-icons:nestjs',
  'TypeScript': 'simple-icons:typescript',
  'JWT': 'mdi:key-chain',
  'bcrypt': 'mdi:shield-lock',
  'Swagger': 'simple-icons:swagger',

  'PostgreSQL': 'simple-icons:postgresql',
  'MySQL': 'simple-icons:mysql',
  'Prisma ORM': 'simple-icons:prisma',
  'Sequelize': 'simple-icons:sequelize',

  'Git': 'simple-icons:git',
  'Gitflow': 'mdi:source-branch',
  'Docker': 'simple-icons:docker',

  'Windows 10 / 11': 'simple-icons:windows',
  'Linux (Debian)': 'simple-icons:debian',

  'LAN': 'mdi:lan',
  'TCP/IP': 'mdi:lan-connect',
  'DHCP / DNS': 'mdi:dns',
  'VPN': 'mdi:vpn',
  'Diagnostic réseau': 'mdi:lan-check',

  'Support N1/N2': 'mdi:headset',
  'Sécurisation des postes': 'mdi:shield-check',
  'Dépannage matériel': 'mdi:laptop',
  'Documentation technique': 'mdi:file-document',

  'GLPI': 'mdi:clipboard-text',
  'Git/GitHub': 'simple-icons:github',

  'Sécurité réseau': 'mdi:shield-network',
  'Sécurité des systèmes Linux': 'mdi:linux',
  'Sécurité des applications Web (OWASP, JWT, bcrypt)': 'mdi:web-check'
}

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
  <section ref="sectionRef" :class="['section', { 'section--visible': sectionVisible }]" id="skills">
    <p class="section-eyebrow">compétences</p>
    <h2 class="section-title">Deux terrains, un seul niveau d'exigence</h2>

    <div class="skills-columns">
      <div class="skill-block skill-block--dev">
        <h3>Développement</h3>
        <div
          class="skill-group glass-card"
          v-for="group in devSkills"
          :key="group.title"
          :class="{ 'is-visible': sectionVisible }"
        >
          <div class="skill-group-header">
            <h4>{{ group.title }}</h4>
          </div>

          <div class="tag-row">
            <div class="tag" v-for="tag in group.tags" :key="tag.name">
              <span class="tag-icon">
                <Icon
                  :icon="techIcons[tag.name] || 'mdi:code-tags'"
                  width="24"
                  height="24"
                  aria-hidden="true"
                />
              </span>
              <div class="tag-content">
                <strong>{{ tag.name }}</strong>
                <div class="tag-progress" aria-hidden="true">
                  <span class="tag-progress__fill" :style="{ width: sectionVisible ? tag.level + '%' : '0%' }"></span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="skill-block skill-block--net">
        <h3>Réseaux &amp; support IT</h3>
        <div
          class="skill-group glass-card"
          v-for="group in netSkills"
          :key="group.title"
          :class="{ 'is-visible': sectionVisible, 'skill-group--compact': group.title === 'Cybersécurité' || group.title === 'Réseaux' }"
        >
          <div class="skill-group-header">
            <h4>{{ group.title }}</h4>
          </div>

          <div class="tag-row">
            <div class="tag" v-for="tag in group.tags" :key="tag.name">
              <span class="tag-icon">
                <Icon
                  :icon="techIcons[tag.name] || 'mdi:code-tags'"
                  width="24"
                  height="24"
                  aria-hidden="true"
                />
              </span>
              <div class="tag-content">
                <strong>{{ tag.name }}</strong>
                <span v-if="tag.description" class="tag-description">{{ tag.description }}</span>
                <div class="tag-progress" aria-hidden="true">
                  <span class="tag-progress__fill" :style="{ width: sectionVisible ? tag.level + '%' : '0%' }"></span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
  color: #000;
  margin-bottom: 12px;
}
.section-title {
  font-size: 28px;
  max-width: 640px;
  margin-bottom: 44px;
}
.skills-columns {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 28px;
}
.skill-block {
  background: transparent;
  border: none;
  padding: 0;
}
.skill-block h3 {
  font-size: 20px;
  margin-bottom: 24px;
}
.skill-group {
  margin-bottom: 22px;
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}
.skill-group.is-visible {
  opacity: 1;
  transform: translateY(0);
}
.skill-group--compact {
  margin-bottom: 16px;
  padding: 18px;
}
.skill-group--compact .skill-group-header {
  margin-bottom: 12px;
}
.skill-group--compact .tag-row {
  gap: 10px;
}
.skill-group--compact .tag {
  padding: 12px;
  border-radius: 14px;
}
.skill-group--compact .tag-content strong {
  font-size: 13px;
  margin-bottom: 4px;
}
.skill-group--compact .tag-description {
  font-size: 11px;
  margin-bottom: 8px;
}
.skill-group--compact .tag-progress {
  height: 5px;
}
.glass-card {
  background: #ffffff;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 18px;
  backdrop-filter: blur(18px);
  box-shadow: 0 24px 48px rgba(0, 0, 0, 0.08);
  padding: 24px;
}
.skill-group-header {
  display: grid;
  gap: 12px;
  margin-bottom: 18px;
}
.skill-group h4 {
  font-size: 13px;
  color: var(--slate);
  text-transform: uppercase;
  letter-spacing: 0.12em;
}
.tag-row {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}
.tag {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 12px;
  align-items: start;
  padding: 16px;
  border-radius: 16px;
  background: #ffffff;
  color: #111;
  min-width: 0;
}
.tag-icon {
  display: inline-flex;
  width: 1.4em;
  height: 1.4em;
  color: #000;
  flex-shrink: 0;
}
.tag-icon svg {
  width: 100%;
  height: 100%;
}
.tag-content strong {
  display: block;
  font-size: 14px;
  margin-bottom: 6px;
}
.tag-description {
  display: block;
  font-size: 12px;
  line-height: 1.45;
  color: var(--slate);
  margin-bottom: 10px;
}
.tag-progress {
  width: 100%;
  height: 6px;
  border-radius: 999px;
  background: rgba(0, 0, 0, 0.08);
  overflow: hidden;
}
.tag-progress__fill {
  display: block;
  height: 100%;
  width: 0;
  background: linear-gradient(90deg, rgba(0, 0, 0, 0.95), rgba(56, 56, 56, 0.95));
  border-radius: 999px;
  transition: width 1.2s ease;
}
@media (max-width: 900px) {
  .section {
    padding: 64px 18px;
  }

  .section-title {
    font-size: 26px;
    margin-bottom: 32px;
  }

  .skills-columns {
    grid-template-columns: 1fr;
    gap: 24px;
  }
}
@media (max-width: 700px) {
  .section {
    padding: 52px 16px;
  }

  .section-title {
    font-size: 24px;
  }

  .tag-row {
    grid-template-columns: 1fr;
  }
}
</style>
