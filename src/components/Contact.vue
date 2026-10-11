<script setup>
import { ref } from 'vue'

const form = ref({
  fullName: '',
  email: '',
  message: '',
})

const submitted = ref(false)
const loading   = ref(false)

function handleSubmit() {
  if (!form.value.fullName || !form.value.email || !form.value.message) return
  loading.value = true
  // Simulasi submit
  setTimeout(() => {
    loading.value  = false
    submitted.value = true
    form.value = { fullName: '', email: '', message: '' }
    setTimeout(() => { submitted.value = false }, 4000)
  }, 800)
}

const contactInfo = [
  {
    icon: 'email',
    label: 'Email',
    value: 'ridhodwiki768@gmail.com',
    href: 'mailto:ridhodwiki768@gmail.com',
  },
  {
    icon: 'phone',
    label: 'Phone',
    value: '+62 895 2635 2118',
    href: 'tel:+62895263521118',
  },
  {
    icon: 'location',
    label: 'Location',
    value: 'Pemalang, Indonesia',
    href: null,
  },
]
</script>

<template>
  <section id="contact" class="contact-section" aria-label="Contact">

    <!-- =============================================
         BANNER — dark wireframe mesh (sama dengan section lain)
         ============================================= -->
    <div class="contact-banner">
      <div class="banner-canvas-wrap" aria-hidden="true">
        <canvas ref="bannerCanvas" class="banner-canvas"></canvas>
      </div>

      <!-- Ikon logo kecil -->
      <div class="banner-inner">
        <div class="banner-logo-icon" aria-hidden="true">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="#9EFF00" aria-hidden="true">
            <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
          </svg>
        </div>
        <h2 class="banner-title">
          Thank you for your Interest in
          <span class="title-accent">Ridho Dwiki.</span>
        </h2>
        <p class="banner-sub">
          We would love to hear from you and discuss how we can help bring your digital ideas to life.
          Here are the different ways you can get in touch with us.
        </p>
        <a href="#contact-form" class="btn-lime-banner">Start Project</a>
      </div>
    </div>

    <!-- =============================================
         CONTACT BODY — info kiri + form kanan
         ============================================= -->
    <div class="contact-body" id="contact-form">
      <div class="contact-grid">

        <!-- LEFT: Contact info cards -->
        <div class="contact-info-col">
          <h3 class="info-heading">Contact Information</h3>
          <p class="info-sub">Hubungi saya langsung melalui kanal berikut.</p>

          <div class="info-cards">
            <a
              v-for="item in contactInfo"
              :key="item.label"
              :href="item.href || undefined"
              class="info-card"
              :class="{ 'no-link': !item.href }"
              :aria-label="item.label + ': ' + item.value"
            >
              <div class="info-icon-box">
                <!-- Email -->
                <svg v-if="item.icon === 'email'" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#9EFF00" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                  <rect x="2" y="4" width="20" height="16" rx="2"/>
                  <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
                </svg>
                <!-- Phone -->
                <svg v-else-if="item.icon === 'phone'" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#9EFF00" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                  <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.6 1.27h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L7.91 8.9a16 16 0 0 0 6 6l.96-.96a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/>
                </svg>
                <!-- Location -->
                <svg v-else width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#9EFF00" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                  <path d="M20 10c0 6-8 12-8 12S4 16 4 10a8 8 0 1 1 16 0z"/>
                  <circle cx="12" cy="10" r="3"/>
                </svg>
              </div>
              <div class="info-text">
                <span class="info-label">{{ item.label }}</span>
                <span class="info-value">{{ item.value }}</span>
              </div>
              <svg v-if="item.href" class="info-arrow" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M7 17L17 7M7 7h10v10"/>
              </svg>
            </a>
          </div>

          <!-- Social links -->
          <div class="social-row" aria-label="Social media">
            <a href="https://github.com/" target="_blank" rel="noopener noreferrer" class="social-btn" aria-label="GitHub">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0 1 12 6.844a9.59 9.59 0 0 1 2.504.337c1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.02 10.02 0 0 0 22 12.017C22 6.484 17.522 2 12 2z"/>
              </svg>
            </a>
            <a href="https://linkedin.com/" target="_blank" rel="noopener noreferrer" class="social-btn" aria-label="LinkedIn">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
              </svg>
            </a>
            <a href="https://instagram.com/" target="_blank" rel="noopener noreferrer" class="social-btn" aria-label="Instagram">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- RIGHT: Contact Form -->
        <div class="contact-form-col">
          <form class="contact-form" @submit.prevent="handleSubmit" novalidate aria-label="Send a message">

            <!-- Row 1: Full Name + Email -->
            <div class="form-row">
              <div class="form-group">
                <label class="form-label" for="cf-name">Full Name</label>
                <input
                  id="cf-name"
                  v-model="form.fullName"
                  type="text"
                  class="form-input"
                  placeholder="Type here"
                  autocomplete="name"
                  required
                />
              </div>
              <div class="form-group">
                <label class="form-label" for="cf-email">Email</label>
                <input
                  id="cf-email"
                  v-model="form.email"
                  type="email"
                  class="form-input"
                  placeholder="Type here"
                  autocomplete="email"
                  required
                />
              </div>
            </div>

            <!-- Row 2: Message -->
            <div class="form-group">
              <label class="form-label" for="cf-message">Your Message</label>
              <textarea
                id="cf-message"
                v-model="form.message"
                class="form-input form-textarea"
                placeholder="Type here"
                rows="5"
                required
              ></textarea>
            </div>

            <!-- Success notice -->
            <transition name="fade">
              <p v-if="submitted" class="form-success" role="status">
                ✓ Pesan berhasil dikirim! Saya akan segera menghubungi kamu.
              </p>
            </transition>

            <button type="submit" class="btn-submit" :disabled="loading">
              <span v-if="!loading">Submit</span>
              <span v-else class="loading-dots">Sending…</span>
            </button>

          </form>
        </div>

      </div>
    </div>

  </section>
</template>

<script>
export default {
  mounted() {
    this.drawMesh()
    window.addEventListener('resize', this.drawMesh)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.drawMesh)
  },
  methods: {
    drawMesh() {
      const canvas = this.$el.querySelector('.banner-canvas')
      if (!canvas) return
      const ctx = canvas.getContext('2d')
      const W = canvas.offsetWidth  || 1200
      const H = canvas.offsetHeight || 340
      canvas.width  = W
      canvas.height = H

      const COLS = 72
      const ROWS = 26
      const cellW = W / COLS
      const cellH = H / ROWS

      const heights = []
      for (let r = 0; r <= ROWS; r++) {
        heights[r] = []
        for (let c = 0; c <= COLS; c++) {
          const nx = c / COLS
          const ny = r / ROWS
          const peak1 = Math.exp(-((nx - 0.25) ** 2 + (ny - 0.85) ** 2) * 12) * 160
          const peak2 = Math.exp(-((nx - 0.75) ** 2 + (ny - 0.88) ** 2) * 15) * 130
          const wave  = Math.sin(nx * Math.PI * 4)   * 10 + Math.sin(ny * Math.PI * 2.5) * 6
          heights[r][c] = peak1 + peak2 + wave
        }
      }

      const fov   = 480
      const viewZ = -160
      const project = (x3, y3, z3) => {
        const s = fov / (fov + z3 - viewZ)
        return { x: W / 2 + x3 * s, y: H * 0.78 + y3 * s }
      }

      ctx.clearRect(0, 0, W, H)
      ctx.fillStyle = '#080808'
      ctx.fillRect(0, 0, W, H)

      for (let r = 0; r < ROWS; r++) {
        for (let c = 0; c < COLS; c++) {
          const x3  = (c     - COLS / 2) * cellW * 0.88
          const z3  = (r     - ROWS * 0.05) * cellH * 1.05
          const y3  = -heights[r][c]
          const x3r = (c + 1 - COLS / 2) * cellW * 0.88
          const y3r = -heights[r][c + 1]
          const z3d = (r + 1 - ROWS * 0.05) * cellH * 1.05
          const y3d = -heights[r + 1][c]

          const p  = project(x3,  y3,  z3)
          const pr = project(x3r, y3r, z3)
          const pd = project(x3,  y3d, z3d)

          const depth = r / ROWS
          const alpha = 0.07 + (1 - depth) * 0.35
          ctx.strokeStyle = `rgba(158,255,0,${alpha})`
          ctx.lineWidth   = depth < 0.25 ? 0.32 : 0.58

          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pr.x, pr.y); ctx.stroke()
          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pd.x, pd.y); ctx.stroke()
        }
      }

      // Bottom + top fades
      const gBot = ctx.createLinearGradient(0, H * 0.45, 0, H)
      gBot.addColorStop(0, 'rgba(8,8,8,0)')
      gBot.addColorStop(1, 'rgba(8,8,8,1)')
      ctx.fillStyle = gBot
      ctx.fillRect(0, H * 0.45, W, H * 0.55)

      const gTop = ctx.createLinearGradient(0, 0, 0, H * 0.4)
      gTop.addColorStop(0, 'rgba(8,8,8,1)')
      gTop.addColorStop(1, 'rgba(8,8,8,0)')
      ctx.fillStyle = gTop
      ctx.fillRect(0, 0, W, H * 0.4)
    }
  }
}
</script>

<style scoped>
/* =========================================
   CONTACT SECTION
   ========================================= */
.contact-section {
  width: 100%;
  background: #0e0e0e;
  border-top: 1px solid #1e1e1e;
}

/* =========================================
   BANNER
   ========================================= */
.contact-banner {
  position: relative;
  width: 100%;
  min-height: 340px;
  background: #080808;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  isolation: isolate;
}

.contact-banner::after {
  content: "";
  position: absolute;
  inset: 0;
  background-image: radial-gradient(rgba(255,255,255,0.04) 1px, transparent 1px);
  background-size: 14px 14px;
  opacity: 0.4;
  pointer-events: none;
  z-index: 1;
}

.banner-canvas-wrap {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}

.banner-canvas {
  width: 100%;
  height: 100%;
  display: block;
}

.banner-inner {
  position: relative;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 3.5rem 1.5rem;
  max-width: 700px;
  gap: 1.1rem;
}

.banner-logo-icon {
  width: 52px;
  height: 52px;
  background: #1a2208;
  border: 1px solid #2c3d0a;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 20px rgba(158,255,0,0.12);
}

.banner-title {
  font-family: var(--font-main, sans-serif);
  font-size: clamp(1.5rem, 3.2vw, 2.1rem);
  font-weight: 700;
  color: #ffffff;
  letter-spacing: -0.02em;
  line-height: 1.25;
  margin: 0;
}

.title-accent {
  color: #9EFF00;
}

.banner-sub {
  font-family: var(--font-main, sans-serif);
  font-size: 0.82rem;
  color: #7a7a7a;
  line-height: 1.7;
  max-width: 580px;
  margin: 0;
}

.btn-lime-banner {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-main, sans-serif);
  font-size: 0.9rem;
  font-weight: 600;
  color: #111;
  background-color: #9EFF00;
  border: 1px solid transparent;
  padding: 0.65rem 1.8rem;
  border-radius: 7px;
  text-decoration: none;
  transition: all 0.2s ease;
  box-shadow: 0 2px 14px rgba(158,255,0,0.2);
  margin-top: 0.4rem;
}

.btn-lime-banner:hover {
  background-color: #acff24;
  transform: translateY(-2px);
  box-shadow: 0 6px 22px rgba(158,255,0,0.32);
}

/* =========================================
   CONTACT BODY
   ========================================= */
.contact-body {
  width: 100%;
  background: #111111;
  border-top: 1px solid #1e1e1e;
  padding: 4rem 2rem 5rem;
}

.contact-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 360px 1fr;
  gap: 4rem;
  align-items: start;
}

/* =========================================
   LEFT — Info Cards
   ========================================= */
.contact-info-col {
  display: flex;
  flex-direction: column;
  gap: 1.6rem;
}

.info-heading {
  font-family: var(--font-main, sans-serif);
  font-size: 1.2rem;
  font-weight: 700;
  color: #f0f0f0;
  letter-spacing: -0.01em;
}

.info-sub {
  font-family: var(--font-main, sans-serif);
  font-size: 0.84rem;
  color: #6a6a6a;
  line-height: 1.6;
  margin-top: -0.8rem;
}

.info-cards {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  background: #151515;
  border: 1px solid #242424;
  border-radius: 10px;
  padding: 1rem 1.1rem;
  text-decoration: none;
  color: inherit;
  transition: border-color 0.2s, background 0.2s;
}

.info-card:not(.no-link):hover {
  border-color: #333;
  background: #1a1a1a;
}

.info-card.no-link {
  cursor: default;
}

.info-icon-box {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
  background: #1a2208;
  border: 1px solid #2c3d0a;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.info-text {
  display: flex;
  flex-direction: column;
  gap: 0.2rem;
  flex: 1;
  min-width: 0;
}

.info-label {
  font-family: var(--font-main, sans-serif);
  font-size: 0.72rem;
  font-weight: 500;
  color: #555;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.info-value {
  font-family: var(--font-main, sans-serif);
  font-size: 0.9rem;
  font-weight: 500;
  color: #d0d0d0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.info-arrow {
  color: #444;
  flex-shrink: 0;
  transition: color 0.2s;
}

.info-card:hover .info-arrow {
  color: #9EFF00;
}

/* Social row */
.social-row {
  display: flex;
  gap: 0.75rem;
  margin-top: 0.4rem;
}

.social-btn {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  background: #151515;
  border: 1px solid #252525;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #888;
  text-decoration: none;
  transition: color 0.2s, border-color 0.2s, background 0.2s;
}

.social-btn:hover {
  color: #9EFF00;
  border-color: #9EFF00;
  background: #1a2208;
}

/* =========================================
   RIGHT — Contact Form
   ========================================= */
.contact-form-col {
  padding-top: 0.25rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.55rem;
}

.form-label {
  font-family: var(--font-main, sans-serif);
  font-size: 0.82rem;
  font-weight: 500;
  color: #8a8a8a;
  letter-spacing: 0.01em;
}

.form-input {
  width: 100%;
  background: #151515;
  border: 1px solid #272727;
  border-radius: 8px;
  padding: 0.8rem 1rem;
  font-family: var(--font-main, sans-serif);
  font-size: 0.9rem;
  color: #e0e0e0;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
  resize: none;
}

.form-input::placeholder {
  color: #404040;
}

.form-input:focus {
  border-color: #9EFF00;
  box-shadow: 0 0 0 3px rgba(158,255,0,0.08);
}

.form-textarea {
  min-height: 130px;
  resize: vertical;
  line-height: 1.6;
}

.form-success {
  font-family: var(--font-main, sans-serif);
  font-size: 0.85rem;
  color: #9EFF00;
  background: rgba(158,255,0,0.07);
  border: 1px solid rgba(158,255,0,0.2);
  border-radius: 7px;
  padding: 0.7rem 1rem;
}

.btn-submit {
  align-self: flex-start;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-main, sans-serif);
  font-size: 0.95rem;
  font-weight: 600;
  color: #111;
  background-color: #9EFF00;
  border: none;
  padding: 0.8rem 2.4rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 2px 14px rgba(158,255,0,0.18);
}

.btn-submit:hover:not(:disabled) {
  background-color: #acff24;
  transform: translateY(-2px);
  box-shadow: 0 6px 22px rgba(158,255,0,0.32);
}

.btn-submit:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

/* Transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* =========================================
   RESPONSIVE
   ========================================= */
@media (max-width: 900px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }

  .contact-info-col {
    max-width: 520px;
    margin: 0 auto;
    width: 100%;
  }
}

@media (max-width: 600px) {
  .contact-body {
    padding: 2.8rem 1.25rem 3.5rem;
  }

  .form-row {
    grid-template-columns: 1fr;
  }

  .contact-banner {
    min-height: 280px;
  }

  .banner-title {
    font-size: 1.4rem;
  }

  .btn-submit {
    width: 100%;
  }
}
</style>
