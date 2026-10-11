<script setup>
// About section — personal info & stats
const stats = [
  { value: '10+', label: 'Projects Completed' },
  { value: '3+',  label: 'Years Learning' },
  { value: '5+',  label: 'Technologies Mastered' },
]

const skills = [
  'Vue.js', 'Figma', 'Python', 'ESP32 / IoT',
  'System Analysis', 'UI/UX Design', 'MySQL', 'Tailwind CSS',
]

const profilePhoto = '/images/profile.jpg'
</script>

<template>
  <!-- =============================================
       ABOUT BANNER (wireframe background — same pattern as Services & Work)
       ============================================= -->
  <section id="about" class="about-section" aria-label="About Me">

    <div class="about-banner">
      <div class="banner-canvas-wrap" aria-hidden="true">
        <canvas ref="bannerCanvas" class="banner-canvas"></canvas>
      </div>
      <div class="banner-inner">
        <h2 class="banner-title">About Me</h2>
        <p class="banner-sub">
          Kenalan lebih dekat — siapa saya, apa yang saya kerjakan, dan mengapa saya bersemangat membangun solusi digital.
        </p>
      </div>
    </div>

    <!-- =============================================
         ABOUT CONTENT — 2 column: photo left, info right
         ============================================= -->
    <div class="about-body">
      <div class="about-grid">

        <!-- LEFT: Photo + accent frame -->
        <div class="about-photo-col" aria-hidden="true">
          <div class="photo-frame">
            <img
              :src="profilePhoto"
              alt="Foto Profil Ridho Dwiki Zakaria"
              class="profile-img"
            />
            <div class="photo-accent-dot top-right" aria-hidden="true"></div>
            <div class="photo-accent-line bottom-left" aria-hidden="true"></div>
          </div>

          <!-- Stats below photo -->
          <div class="stats-row">
            <div
              v-for="stat in stats"
              :key="stat.label"
              class="stat-item"
            >
              <span class="stat-value">{{ stat.value }}</span>
              <span class="stat-label">{{ stat.label }}</span>
            </div>
          </div>
        </div>

        <!-- RIGHT: Bio + skills -->
        <div class="about-info-col">
          <p class="about-tag">— Hello, I'm</p>
          <h3 class="about-name">
            Ridho Dwiki Zakaria<br />
            <span class="name-accent">Informatics Student</span>
          </h3>

          <p class="about-bio">
            Saya adalah mahasiswa Universitas PGRI Semarang Program Studi Teknik Informatika
            Fakultas Teknik dan Informatika. Saya memiliki minat besar dalam dunia teknologi
            informasi, terutama di bidang <strong>pemrograman</strong> dan
            <strong>pengembangan sistem</strong>. Saya senang mengeksplorasi hal baru yang
            berkaitan dengan <strong>desain antarmuka</strong>, sistem digital, dan teknologi kreatif.
          </p>

          <!-- Skills chips -->
          <div class="skills-wrap" aria-label="Skills">
            <span
              v-for="skill in skills"
              :key="skill"
              class="skill-chip"
            >{{ skill }}</span>
          </div>

          <!-- CTA -->
          <div class="about-actions">
            <a href="#contact" class="btn-lime">Let's Talk</a>
            <a
              href="/cv-muhammad-rafi.pdf"
              download
              class="btn-outline"
              aria-label="Download CV"
            >Download CV</a>
          </div>
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
      const H = canvas.offsetHeight || 280
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
          const peak1 = Math.exp(-((nx - 0.28) ** 2 + (ny - 0.85) ** 2) * 13) * 150
          const peak2 = Math.exp(-((nx - 0.72) ** 2 + (ny - 0.9)  ** 2) * 16) * 120
          const wave  = Math.sin(nx * Math.PI * 3.5) * 9 + Math.sin(ny * Math.PI * 2.5) * 5
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
      ctx.fillStyle = '#0a0a0a'
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
          const alpha = 0.08 + (1 - depth) * 0.32
          ctx.strokeStyle = `rgba(158,255,0,${alpha})`
          ctx.lineWidth   = depth < 0.25 ? 0.35 : 0.6

          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pr.x, pr.y); ctx.stroke()
          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pd.x, pd.y); ctx.stroke()
        }
      }

      // Bottom fade
      const gBot = ctx.createLinearGradient(0, H * 0.45, 0, H)
      gBot.addColorStop(0, 'rgba(10,10,10,0)')
      gBot.addColorStop(1, 'rgba(10,10,10,1)')
      ctx.fillStyle = gBot
      ctx.fillRect(0, H * 0.45, W, H * 0.55)

      // Top fade
      const gTop = ctx.createLinearGradient(0, 0, 0, H * 0.4)
      gTop.addColorStop(0, 'rgba(10,10,10,1)')
      gTop.addColorStop(1, 'rgba(10,10,10,0)')
      ctx.fillStyle = gTop
      ctx.fillRect(0, 0, W, H * 0.4)
    }
  }
}
</script>

<style scoped>
/* =========================================
   ABOUT SECTION WRAPPER
   ========================================= */
.about-section {
  width: 100%;
  background: #111111;
  border-top: 1px solid #1e1e1e;
}

/* =========================================
   BANNER — identical pattern to Services & Work
   ========================================= */
.about-banner {
  position: relative;
  width: 100%;
  min-height: 260px;
  background: #0a0a0a;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  isolation: isolate;
}

.about-banner::after {
  content: "";
  position: absolute;
  inset: 0;
  background-image: radial-gradient(rgba(255,255,255,0.055) 1px, transparent 1px);
  background-size: 14px 14px;
  opacity: 0.35;
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
  text-align: center;
  padding: 3.2rem 1.5rem;
  max-width: 760px;
}

.banner-title {
  font-family: var(--font-main, sans-serif);
  font-size: clamp(1.7rem, 3.5vw, 2.2rem);
  font-weight: 700;
  color: #fff;
  letter-spacing: -0.02em;
  margin-bottom: 0.9rem;
}

.banner-sub {
  font-family: var(--font-main, sans-serif);
  font-size: 0.82rem;
  font-weight: 400;
  color: #9a9a9a;
  line-height: 1.7;
  max-width: 640px;
  margin: 0 auto;
}

/* =========================================
   ABOUT BODY — max-width matches cards-grid (1200px)
   ========================================= */
.about-body {
  width: 100%;
  background: #111111;
  border-top: 1px solid #1e1e1e;
  padding: 4rem 2rem 5rem;
}

.about-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 380px 1fr;
  gap: 4rem;
  align-items: start;
}

/* =========================================
   LEFT COLUMN — Photo
   ========================================= */
.about-photo-col {
  display: flex;
  flex-direction: column;
  gap: 2.4rem;
}

.photo-frame {
  position: relative;
  width: 100%;
  aspect-ratio: 4 / 5;
  border-radius: 16px;
  border: 1px solid #2a2a2a;
  background: #151515;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.photo-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  opacity: 0.35;
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center top;
  display: block;
}

/* Decorative accent dots/lines on the frame */
.photo-accent-dot {
  position: absolute;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #9EFF00;
  opacity: 0.7;
}

.photo-accent-dot.top-right {
  top: 16px;
  right: 16px;
}

.photo-accent-line {
  position: absolute;
  bottom: 20px;
  left: 20px;
  width: 40px;
  height: 2px;
  background: linear-gradient(90deg, #9EFF00, transparent);
}

/* Stats row */
.stats-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background: #1e1e1e;
  border-radius: 10px;
  overflow: hidden;
  border: 1px solid #1e1e1e;
}

.stat-item {
  background: #151515;
  padding: 1.25rem 0.75rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.35rem;
  transition: background 0.2s;
}

.stat-item:hover {
  background: #1a1a1a;
}

.stat-value {
  font-family: var(--font-main, sans-serif);
  font-size: 1.5rem;
  font-weight: 700;
  color: #9EFF00;
  letter-spacing: -0.02em;
  line-height: 1;
}

.stat-label {
  font-family: var(--font-main, sans-serif);
  font-size: 0.72rem;
  font-weight: 400;
  color: #6a6a6a;
  text-align: center;
  line-height: 1.3;
}

/* =========================================
   RIGHT COLUMN — Bio
   ========================================= */
.about-info-col {
  display: flex;
  flex-direction: column;
  gap: 1.4rem;
  padding-top: 0.5rem;
}

.about-tag {
  font-family: var(--font-main, sans-serif);
  font-size: 0.82rem;
  font-weight: 400;
  color: #9EFF00;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

.about-name {
  font-family: var(--font-main, sans-serif);
  font-size: clamp(1.8rem, 3.2vw, 2.6rem);
  font-weight: 700;
  color: #ffffff;
  letter-spacing: -0.03em;
  line-height: 1.15;
}

.name-accent {
  color: #6b6b6b;
  font-weight: 400;
  font-size: 0.82em;
}

.about-bio {
  font-family: var(--font-main, sans-serif);
  font-size: 0.92rem;
  font-weight: 400;
  color: #7a7a7a;
  line-height: 1.8;
}

.about-bio strong {
  color: #c0c0c0;
  font-weight: 500;
}

/* =========================================
   SKILL CHIPS
   ========================================= */
.skills-wrap {
  display: flex;
  flex-wrap: wrap;
  gap: 0.55rem;
  margin-top: 0.4rem;
}

.skill-chip {
  display: inline-flex;
  align-items: center;
  padding: 0.38rem 0.9rem;
  background-color: #1a1a1a;
  border: 1px solid #2a2a2a;
  border-radius: 6px;
  font-family: var(--font-main, sans-serif);
  font-size: 0.82rem;
  font-weight: 500;
  color: #c0c0c0;
  letter-spacing: 0.01em;
  transition: border-color 0.2s, color 0.2s;
}

.skill-chip:hover {
  border-color: #9EFF00;
  color: #9EFF00;
}

/* =========================================
   CTA BUTTONS — reuse identical style from Hero
   ========================================= */
.about-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
  margin-top: 0.6rem;
}

.btn-lime {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-main, sans-serif);
  font-size: 0.97rem;
  font-weight: 600;
  color: #111111;
  background-color: #9eff00;
  border: 1px solid transparent;
  padding: 0.75rem 1.75rem;
  border-radius: 8px;
  text-decoration: none;
  transition: all 0.2s ease;
  box-shadow: 0 2px 14px rgba(158, 255, 0, 0.18);
}

.btn-lime:hover {
  background-color: #acff24;
  transform: translateY(-2px);
  box-shadow: 0 6px 22px rgba(158, 255, 0, 0.32);
}

.btn-outline {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-main, sans-serif);
  font-size: 0.97rem;
  font-weight: 500;
  color: #e8e8e8;
  background-color: transparent;
  border: 1px solid #3a3a3a;
  padding: 0.75rem 1.75rem;
  border-radius: 8px;
  text-decoration: none;
  transition: all 0.2s ease;
}

.btn-outline:hover {
  background-color: #1e1e1e;
  border-color: #555;
  color: #ffffff;
}

/* =========================================
   RESPONSIVE
   ========================================= */
@media (max-width: 900px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }

  .about-photo-col {
    max-width: 420px;
    margin: 0 auto;
    width: 100%;
  }

  .photo-frame {
    aspect-ratio: 1 / 1;
  }
}

@media (max-width: 600px) {
  .about-body {
    padding: 2.8rem 1.25rem 3.5rem;
  }

  .about-name {
    font-size: 1.85rem;
  }

  .stats-row {
    grid-template-columns: repeat(3, 1fr);
  }

  .stat-value {
    font-size: 1.25rem;
  }

  .about-banner {
    min-height: 220px;
  }

  .banner-sub {
    font-size: 0.78rem;
  }
}
</style>
