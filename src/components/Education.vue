<script setup>
import { ref, onMounted } from 'vue'

const diplomas = [
  { title: 'Licence en télécommunication', date: '2025 – 2026', org: 'Université CNTEMAD — Réseaux et transmission' },
  { title: 'DTS / BTS en télécommunication', date: '2023 – 2024', org: 'Université CNTEMAD — Réseaux et transmission' },
  { title: 'Baccalauréat technique', date: '2021 – 2022', org: 'Lycée technique professionnelle' }
]

const certifications = [
  { icon: 'CFT', title: 'Cybersécurité', org: 'CFT — 2025' },
  { icon: 'MI', title: 'Maintenance informatique', org: 'MITECH — 2025' },
  { icon: 'ODC', title: 'IoT: Découvré les bases des objets connectés', org: 'Orange Digital Center — 2025' }
]

const languages = [
  { name: 'Malagasy', level: 95 },
  { name: 'Français', level: 85 },
  { name: 'Anglais', level: 55 }
]

const sectionRef = ref(null)
const visibleItems = ref([])

onMounted(() => {
  const items = sectionRef.value?.querySelectorAll('.reveal-item') || []

  const observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const id = entry.target.dataset.revealId
          if (id && !visibleItems.value.includes(id)) {
            visibleItems.value.push(id)
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
  <section ref="sectionRef" class="section" id="education">
    <p class="section-eyebrow">formation</p>
    <h2 class="section-title">Formation &amp; certifications</h2>

    <div class="edu-grid">
      <div>
        <h3>Diplômes</h3>
        <div class="timeline timeline--compact">
          <div
            class="timeline-item reveal-item"
            v-for="(d, index) in diplomas"
            :key="d.title"
            :data-reveal-id="`diploma-${index}`"
            :class="{ 'timeline-item--visible': visibleItems.includes(`diploma-${index}`) }"
          >
            <div class="timeline-marker timeline-marker--dev"></div>
            <div class="timeline-content">
              <div class="timeline-head">
                <h4>{{ d.title }}</h4>
                <span class="timeline-date">{{ d.date }}</span>
              </div>
              <p class="timeline-org">{{ d.org }}</p>
            </div>
          </div>
        </div>

        <h3 class="lang-title">Langues</h3>
        <div class="lang-list">
          <div
            class="lang-item reveal-item"
            v-for="(l, index) in languages"
            :key="l.name"
            :data-reveal-id="`lang-${index}`"
            :class="{ 'timeline-item--visible': visibleItems.includes(`lang-${index}`) }"
          >
            <span>{{ l.name }}</span>
            <div class="lang-bar"><i :style="{ width: visibleItems.includes(`lang-${index}`) ? l.level + '%' : '0%' }"></i></div>
          </div>
        </div>
      </div>

      <div>
        <h3>Certifications</h3>
        <div class="cert-list">
          <div
            class="cert-item reveal-item"
            v-for="(c, index) in certifications"
            :key="c.title"
            :data-reveal-id="`cert-${index}`"
            :class="{ 'timeline-item--visible': visibleItems.includes(`cert-${index}`) }"
          >
            <span class="cert-icon">{{ c.icon }}</span>
            <div>
              <h4>{{ c.title }}</h4>
              <p>{{ c.org }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section { padding: clamp(3rem, 5vw, 4rem) 1.5rem; max-width: min(1120px, 100%); margin: 0 auto; min-height: auto; scroll-margin-top: calc(var(--nav-height) + 20px); }
.section-eyebrow { font-family: var(--font-mono); font-size: 13px; color: var(--copper); margin-bottom: 12px; }
.section-title { font-size: 28px; max-width: 640px; margin-bottom: 44px; }
.edu-grid { display: grid; grid-template-columns: 1.2fr 0.8fr; gap: 48px; }
h3 { font-size: 15px; margin-bottom: 20px; }

.timeline { position: relative; padding-left: 28px; }
.timeline::before { content: ''; position: absolute; left: 5px; top: 6px; bottom: 6px; width: 1.5px; background: var(--border-strong); }
.timeline-item { position: relative; margin-bottom: 24px; opacity: 0; transform: translateY(30px); transition: opacity 0.75s ease, transform 0.75s ease; }
.timeline-item--visible { opacity: 1; transform: translateY(0); }
.timeline-marker { position: absolute; left: -28px; top: 4px; width: 11px; height: 11px; border-radius: 50%; background: var(--surface); border: 2px solid var(--teal); }
.timeline-head { display: flex; justify-content: space-between; align-items: baseline; gap: 16px; flex-wrap: wrap; }
.timeline-head h4 { font-size: 14.5px; }
.timeline-date { font-family: var(--font-mono); font-size: 12px; color: var(--slate); white-space: nowrap; }
.timeline-org { color: var(--slate); font-size: 13.5px; }

.cert-list { display: flex; flex-direction: column; gap: 14px; margin-bottom: 36px; }
.cert-item { display: flex; align-items: center; gap: 14px; background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 14px 16px; opacity: 0; transform: translateY(30px); transition: opacity 0.75s ease, transform 0.75s ease; }
.cert-item.timeline-item--visible { opacity: 1; transform: translateY(0); }
.cert-icon { font-family: var(--font-mono); font-size: 11px; color: var(--teal-dark); background: var(--teal-tint); width: 36px; height: 36px; border-radius: 8px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.cert-item h4 { font-size: 14.5px; margin-bottom: 2px; }
.cert-item p { font-size: 13px; color: var(--slate); }

.lang-title { margin-top: 8px; }
.lang-list { display: flex; flex-direction: column; gap: 14px; }
.lang-item { opacity: 0; transform: translateY(30px); transition: opacity 0.75s ease, transform 0.75s ease; }
.lang-item.timeline-item--visible { opacity: 1; transform: translateY(0); }
.lang-item span { display: block; font-size: 13.5px; margin-bottom: 6px; color: var(--slate); }
.lang-bar { height: 5px; border-radius: 4px; background: var(--border); overflow: hidden; }
.lang-bar i { display: block; height: 100%; width: 0; background: var(--teal); border-radius: 4px; transition: width 1s ease; }

@media (max-width: 900px) {
  .section {
    padding: 64px 18px;
  }

  .section-title {
    font-size: 26px;
    margin-bottom: 32px;
  }

  .edu-grid {
    grid-template-columns: 1fr;
    gap: 32px;
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

  .timeline-date {
    white-space: normal;
  }
}

@media (max-width: 700px) {
  .section {
    padding: 52px 16px;
  }

  .section-title {
    font-size: 24px;
  }

  .edu-grid {
    gap: 24px;
  }

  .cert-item {
    flex-wrap: wrap;
    gap: 12px;
  }
}
</style>