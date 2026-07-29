<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { Mail, Phone, MapPin } from 'lucide-vue-next'

const sectionRef = ref(null)
const sectionVisible = ref(false)

function openGmail(event) {
  event.preventDefault()
  const form = event.target
  if (!form.reportValidity()) {
    return
  }

  const fullname = form.fullname.value.trim()
  const email = form.email.value.trim()
  const subjectField = form.subject.value.trim()
  const message = form.message.value.trim()

  const mailtoSubject = encodeURIComponent('Contact depuis mon portfolio')
  const mailtoBody = encodeURIComponent(
    `Bonjour,%0D%0A%0D%0ANom : ${fullname}%0D%0AEmail : ${email}%0D%0ASujet : ${subjectField || '—'}%0D%0A%0D%0AMessage : %0D%0A${message}%0D%0A%0D%0AMerci.`
  )

  window.location.href = `mailto:toumandimbison@gmail.com?subject=${mailtoSubject}&body=${mailtoBody}`
}

let observer
onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry && entry.isIntersecting) {
      sectionVisible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.15 })
  if (sectionRef.value) observer.observe(sectionRef.value)
})
onBeforeUnmount(() => { if (observer) observer.disconnect() })
</script>

<template>
  <section ref="sectionRef" :class="['section-contact', { 'is-visible': sectionVisible }]" id="contact" aria-labelledby="contact-title">
    <div class="contact-grid">
      <div class="contact-left">
        <h2 id="contact-title" class="contact-title">Discutons de votre projet</h2>
        <p class="contact-lead">Une idée, un projet ou une opportunité ? N'hésitez pas à me contacter. Je vous répondrai dans les meilleurs délais.</p>

        <form class="form" @submit.prevent="openGmail" novalidate>
          <div class="form-row">
            <label for="fullname">
              <span class="label-text">Nom complet</span>
              <input id="fullname" name="fullname" type="text" required autocomplete="name" />
            </label>

            <label for="email">
              <span class="label-text">Adresse e-mail</span>
              <input id="email" name="email" type="email" required autocomplete="email" />
            </label>
          </div>

          <label for="subject">
            <span class="label-text">Sujet</span>
            <input id="subject" name="subject" type="text" placeholder="Objet de votre message" />
          </label>

          <label for="message">
            <span class="label-text">Message</span>
            <textarea id="message" name="message" rows="6" required placeholder="Décrivez votre projet"></textarea>
          </label>

          <div class="form-actions">
            <button type="submit" class="submit-btn">Envoyer le message</button>
            <small class="privacy-note">Vos informations restent confidentielles et ne seront jamais partagées.</small>
          </div>
        </form>
      </div>

          <aside class="contact-right" aria-label="Coordonnées">
            <a class="info-card" href="mailto:toumandimbison@gmail.com" aria-label="Envoyer un email">
              <div class="card-icon"><Mail aria-hidden="true" :size="20" :stroke-width="2" /></div>
              <div class="card-body">
                <div class="card-title">EMAIL</div>
                <div class="card-main">toumandimbison@gmail.com</div>
                <div class="card-sub">Réponse sous 24h</div>
              </div>
              <div class="card-arrow" aria-hidden="true">➜</div>
            </a>

            <a class="info-card" href="tel:+261333892217" aria-label="Appeler">
              <div class="card-icon"><Phone aria-hidden="true" :size="20" :stroke-width="2" /></div>
              <div class="card-body">
                <div class="card-title">TÉLÉPHONE</div>
                <div class="card-main">+261 33 38 922 17</div>
                <div class="card-sub">Disponible de 8h à 18h</div>
              </div>
              <div class="card-arrow" aria-hidden="true">➜</div>
            </a>

            <div class="info-card" aria-label="Localisation">
              <div class="card-icon"><MapPin aria-hidden="true" :size="20" :stroke-width="2" /></div>
              <div class="card-body">
                <div class="card-title">LOCALISATION</div>
                <div class="card-main">Fianarantsoa, Madagascar</div>
              </div>
              <div class="card-arrow" aria-hidden="true">➜</div>
            </div>
          </aside>
    </div>
  </section>
</template>

<style scoped>
/* Layout */
.section-contact { padding: clamp(3rem, 5vw, 4rem) 1.5rem 3rem; background: #ffffff; color: #0b0b0b; min-height: auto; scroll-margin-top: calc(var(--nav-height) + 8px); }
.contact-grid { max-width: min(1120px, 100%); margin: 0 auto; display: grid; grid-template-columns: 1fr 360px; gap: clamp(20px, 3vw, 28px); align-items: center; }
.contact-left { display: flex; flex-direction: column; gap: 18px; }
.contact-title { font-family: var(--font-space); font-size: 32px; margin: 0; }
.contact-lead { margin: 0; color: #374151; max-width: 640px; }

/* Form */
.form { display: flex; flex-direction: column; gap: 12px; }
.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
label { display: flex; flex-direction: column; gap: 8px; }
.label-text { font-size: 13px; color: #6b7280; }
input[type="text"], input[type="email"], textarea {
  width: 100%;
  padding: 12px 14px;
  border-radius: 10px;
  border: 1px solid #e6e7e8;
  background: #fff;
  color: #0b0b0b;
  transition: box-shadow .25s ease, border-color .25s ease, transform .15s ease;
  font-size: 14px;
}
textarea { resize: vertical; min-height: 120px; }
input:focus, textarea:focus { outline: none; border-color: #000; box-shadow: 0 6px 24px rgba(2,6,23,0.06); }

.form-actions { display: flex; flex-direction: column; gap: 10px; margin-top: 4px; }
.submit-btn { align-self: start; padding: 12px 20px; border-radius: 12px; border: none; background: #111111; color: #ffffff; font-weight: 700; cursor: pointer; box-shadow: 0 6px 18px rgba(17,17,17,0.08); transition: transform .28s cubic-bezier(.2,.9,.3,1), box-shadow .28s, background .28s; }
.submit-btn:hover, .submit-btn:focus { transform: translateY(-4px); box-shadow: 0 18px 44px rgba(17,17,17,0.12); background: #0b0b0b; }
.privacy-note { font-size: 12px; color: #6b7280; }

/* Right column cards */
.contact-right { display: flex; flex-direction: column; gap: 12px; }
.info-card { display: flex; gap: 12px; align-items: center; padding: 12px 14px; border-radius: 12px; background: #ffffff; border: 1px solid #eef0f2; box-shadow: 0 6px 16px rgba(2,6,23,0.04); text-decoration: none; color: inherit; transition: transform .28s, box-shadow .28s, background .28s; }
.info-card:hover, .info-card:focus { transform: translateY(-6px); box-shadow: 0 20px 50px rgba(2,6,23,0.08); background: #fbfbfb; }
 .card-icon { width: 48px; height: 48px; border-radius: 10px; display: grid; place-items: center; font-size: 20px; background: #ffffff; color: #000; border: 1px solid #eef0f2; transition: background .28s, color .28s, border .28s, transform .28s; }
.card-body { display: flex; flex-direction: column; }
.card-title { font-size: 11px; color: #6b7280; text-transform: uppercase; letter-spacing: 0.06em; }
.card-main { font-weight: 600; font-size: 15px; color: #0b0b0b; }
.card-sub { font-size: 12px; color: #6b7280; }

/* Arrow on the right */
.card-arrow { margin-left: auto; font-size: 16px; color: #000; opacity: 0; transform: translateX(-8px); transition: opacity .28s ease, transform .28s ease, color .28s ease; }
.info-card:hover .card-arrow, .info-card:focus .card-arrow { opacity: 1; transform: none; color: #fff; }

/* Invert icon colors on hover */
.info-card:hover .card-icon, .info-card:focus .card-icon { background: #000; color: #ffffff; border-color: #000; transform: translateY(-2px); }

/* Compact the cards for a premium look */
.info-card { padding: 12px; }
.card-icon { width: 42px; height: 42px; border-radius: 10px; font-size: 18px; }

/* Reveal animation */
.section-contact { opacity: 0; transform: translateY(18px); transition: opacity .7s ease, transform .7s ease; }
.section-contact.is-visible { opacity: 1; transform: none; }

/* Responsive */
@media (max-width: 980px) {
  .section-contact { padding: 56px 18px 40px; }
  .contact-grid { grid-template-columns: 1fr 320px; gap: 20px; }
}
@media (max-width: 760px) {
  .section-contact { padding: 48px 16px 32px; }
  .contact-grid { grid-template-columns: 1fr; }
  .form-row { grid-template-columns: 1fr; }
  .contact-right { order: 2; width: 100%; }
  .contact-left { order: 1; }
  .form-actions { align-items: stretch; }
  .submit-btn { width: 100%; }
}

@media (max-width: 480px) {
  .section-contact { padding: 40px 14px 28px; }
  .form-row { gap: 10px; }
  .submit-btn { width: 100%; }
}
@media (max-width: 480px) {
  .section-contact { padding: 40px 14px 28px; }
}

/* Accessibility focus states */
input:focus-visible, textarea:focus-visible, .submit-btn:focus-visible, .info-card:focus-visible { outline: 3px solid rgba(2,6,23,0.08); outline-offset: 3px; }

</style>