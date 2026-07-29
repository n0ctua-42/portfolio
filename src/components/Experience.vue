<script setup>
import { ref, onMounted } from 'vue'

const experiences = [
  {
    title: 'Technicien réseau & support IT',
    tag: '(stage académique)',
    date: 'Mars 2025 – Juin 2025',
    org: 'Mi-Tech Informatique — Miarinarivo',
    points: [
      "Configuration et maintenance d'un réseau local pour une petite entreprise.",
      "Mise en œuvre de protocoles de sécurité pour protéger les données sensibles.",
      "Résolution de problèmes techniques liés aux réseaux, mise en place de connexions sécurisées pour les clients.",
      "Suivi des performances réseau, documentation des configurations et propositions d'amélioration."
    ]
  },
  {
    title: 'Mentor technologique',
    tag: '(bénévolat)',
    date: '2025',
    org: 'Association des Jeunes',
    points: [
      "Animation d'ateliers d'initiation à l'informatique.",
      "Organisation de sessions de sensibilisation à la cybersécurité.",
      "Assistance à la mise en place de points d'accès Internet communautaires."
    ]
  }
]

const sectionRef = ref(null)
const visibleItems = ref([])

onMounted(() => {
  const items = sectionRef.value?.querySelectorAll('.timeline-item') || []

  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const index = Number(entry.target.dataset.index)
          if (!visibleItems.value.includes(index)) {
            visibleItems.value.push(index)
          }
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.2 }
  )

  items.forEach(item => observer.observe(item))
})
</script>

<template>
  <section ref="sectionRef" class="section" id="experience">
    <p class="section-eyebrow">expérience</p>
    <h2 class="section-title">Parcours professionnel</h2>

    <div class="timeline">
      <div
        class="timeline-item"
        v-for="(exp, index) in experiences"
        :key="exp.title"
        :data-index="index"
        :class="{ 'timeline-item--visible': visibleItems.includes(index) }"
      >
        <div class="timeline-marker"></div>
        <div class="timeline-content">
          <div class="timeline-head">
            <h3>{{ exp.title }} <span>{{ exp.tag }}</span></h3>
            <span class="timeline-date">{{ exp.date }}</span>
          </div>
          <p class="timeline-org">{{ exp.org }}</p>
          <ul>
            <li v-for="point in exp.points" :key="point">{{ point }}</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section { padding: clamp(3rem, 5vw, 4rem) 1.5rem; max-width: min(1120px, 100%); margin: 0 auto; min-height: auto; scroll-margin-top: calc(var(--nav-height) + 20px); }
.section-eyebrow { font-family: var(--font-mono); font-size: 13px; color: var(--copper); margin-bottom: 12px; }
.section-title { font-size: 28px; max-width: 640px; margin-bottom: 44px; }

.timeline { position: relative; padding-left: 28px; }
.timeline::before {
  content: ''; position: absolute; left: 5px; top: 6px; bottom: 6px;
  width: 1.5px; background: var(--border-strong);
}
.timeline-item {
  position: relative;
  margin-bottom: 36px;
  opacity: 0;
  transform: translateY(32px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}
.timeline-item--visible {
  opacity: 1;
  transform: translateY(0);
}
.timeline-item:last-child { margin-bottom: 0; }
.timeline-marker {
  position: absolute; left: -28px; top: 4px;
  width: 11px; height: 11px; border-radius: 50%;
  background: var(--surface); border: 2px solid var(--copper);
}
.timeline-head { display: flex; justify-content: space-between; align-items: baseline; gap: 16px; flex-wrap: wrap; margin-bottom: 4px; }
.timeline-head h3 { font-size: 16px; }
.timeline-head span:not(.timeline-date) { color: var(--slate); font-weight: 400; font-size: 14px; }
.timeline-date { font-family: var(--font-mono); font-size: 12.5px; color: var(--slate); white-space: nowrap; }
.timeline-org { color: var(--copper-dark); font-size: 14px; margin-bottom: 10px; }
.timeline-content ul { display: flex; flex-direction: column; gap: 6px; padding-left: 14px; }
.timeline-content li { font-size: 14.5px; color: var(--slate); }

@media (max-width: 900px) {
  .section {
    padding: 64px 18px;
  }

  .section-title {
    font-size: 26px;
    margin-bottom: 32px;
  }

  .timeline {
    padding-left: 16px;
  }

  .timeline::before {
    left: 0;
  }

  .timeline-marker {
    left: -20px;
  }

  .timeline-head {
    gap: 12px;
  }

  .timeline-date {
    white-space: normal;
  }
}
</style>