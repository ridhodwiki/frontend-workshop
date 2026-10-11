<script setup>
// Tools & Technologies logos (inline SVG untuk Python dan Figma)
const tools = [
  { name: 'Python', id: 'python' },
  { name: 'Figma',  id: 'figma'  },
  { name: 'Python', id: 'python2' },
  { name: 'Figma',  id: 'figma2'  },
  { name: 'Python', id: 'python3' },
  { name: 'Figma',  id: 'figma3'  },
]

// 3 Service cards
const services = [
  {
    id: 'uiux',
    icon: 'pen',
    title: 'UI/UX & Web Design',
    description:
      'Merancang antarmuka aplikasi web dan mobile yang responsif, intuitif, dan berfokus pada pengalaman pengguna.',
  },
  {
    id: 'system',
    icon: 'puzzle',
    title: 'System Analysis & Design (APS)',
    description:
      'Menyusun pemodelan sistem rinci (Use Case, Activity, Sequence Diagram) untuk kebutuhan aplikasi skala UMKM hingga organisasi.',
  },
  {
    id: 'iot',
    icon: 'bolt',
    title: 'IoT & Embedded Systems',
    description:
      'Mengembangkan prototipe perangkat keras pintar (seperti smart lock ESP32) yang terintegrasi langsung dengan bot Telegram atau API web.',
  },
]
</script>

<template>
  <!-- =============================================
       TOOLS & TECHNOLOGIES STRIP
       ============================================= -->
  <section class="tools-strip" aria-label="Tools and Technologies">
    <p class="tools-label">Tools &amp; Technologies I Use</p>
    <div class="tools-track-wrapper">
      <div class="tools-track">
        <!-- Python SVG -->
        <div class="tool-item" title="Python">
          <svg width="56" height="56" viewBox="0 0 256 255" xmlns="http://www.w3.org/2000/svg" aria-label="Python">
            <defs>
              <linearGradient id="py-a" x1="12.959%" x2="79.639%" y1="12.039%" y2="78.201%">
                <stop offset="0" stop-color="#387EB8"/>
                <stop offset="1" stop-color="#366994"/>
              </linearGradient>
              <linearGradient id="py-b" x1="19.128%" x2="90.742%" y1="20.579%" y2="88.429%">
                <stop offset="0" stop-color="#FFE052"/>
                <stop offset="1" stop-color="#FFC331"/>
              </linearGradient>
            </defs>
            <path d="M126.916.072c-64.832 0-60.784 28.115-60.784 28.115l.072 29.128h61.868v8.745H41.631S.145 61.355.145 126.77c0 65.417 36.21 63.097 36.21 63.097h21.61v-30.356s-1.165-36.21 35.632-36.21h61.362s34.475.557 34.475-33.319V33.97S194.67.072 126.916.072zM92.802 19.66a11.12 11.12 0 0 1 11.13 11.13 11.12 11.12 0 0 1-11.13 11.13 11.12 11.12 0 0 1-11.13-11.13 11.12 11.12 0 0 1 11.13-11.13z" fill="url(#py-a)"/>
            <path d="M128.757 254.126c64.832 0 60.784-28.115 60.784-28.115l-.072-29.127H127.6v-8.745h86.441s41.486 4.705 41.486-60.712c0-65.416-36.21-63.096-36.21-63.096h-21.61v30.355s1.165 36.21-35.632 36.21h-61.362s-34.475-.557-34.475 33.32v56.013s-5.235 33.897 62.518 33.897zm34.114-19.586a11.12 11.12 0 0 1-11.13-11.13 11.12 11.12 0 0 1 11.13-11.13 11.12 11.12 0 0 1 11.13 11.13 11.12 11.12 0 0 1-11.13 11.13z" fill="url(#py-b)"/>
          </svg>
        </div>
        <!-- Figma SVG -->
        <div class="tool-item" title="Figma">
          <svg width="48" height="56" viewBox="0 0 38 57" xmlns="http://www.w3.org/2000/svg" aria-label="Figma">
            <path d="M19 28.5a9.5 9.5 0 1 1 19 0 9.5 9.5 0 0 1-19 0z" fill="#1ABCFE"/>
            <path d="M0 47.5A9.5 9.5 0 0 1 9.5 38H19v9.5a9.5 9.5 0 0 1-19 0z" fill="#0ACF83"/>
            <path d="M19 0v19h9.5a9.5 9.5 0 0 0 0-19H19z" fill="#FF7262"/>
            <path d="M0 9.5A9.5 9.5 0 0 0 9.5 19H19V0H9.5A9.5 9.5 0 0 0 0 9.5z" fill="#F24E1E"/>
            <path d="M0 28.5A9.5 9.5 0 0 0 9.5 38H19V19H9.5A9.5 9.5 0 0 0 0 28.5z" fill="#A259FF"/>
          </svg>
        </div>
      </div>
    </div>
  </section>

  <!-- =============================================
       OUR SERVICES BANNER (wireframe background)
       ============================================= -->
  <section id="services" class="services-banner" aria-label="Our Services">
    <div class="banner-canvas-wrapper">
      <canvas ref="bannerCanvas" class="banner-canvas" aria-hidden="true"></canvas>
    </div>
    <div class="banner-content">
      <h2 class="banner-title">Our Services</h2>
      <p class="banner-subtitle">
        Transform your brand with our innovative digital solutions that captivate and engage your audience.
      </p>
    </div>
  </section>

  <!-- =============================================
       3 SERVICE CARDS
       ============================================= -->
  <section class="cards-section" aria-label="Service details">
    <div class="cards-grid">

      <!-- Card: UI/UX & Web Design -->
      <article class="service-card">
        <div class="card-icon-wrap">
          <!-- Pen/pencil icon -->
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="#9eff00" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <path d="M12 20h9"/>
            <path d="M16.5 3.5a2.121 2.121 0 0 1 3 3L7 19l-4 1 1-4 12.5-12.5z"/>
          </svg>
        </div>
        <h3 class="card-title">UI/UX &amp; Web Design</h3>
        <p class="card-desc">
          Merancang antarmuka aplikasi web dan mobile yang responsif, intuitif, dan berfokus pada pengalaman pengguna.
        </p>
        <a href="#contact" class="card-btn">Learn More</a>
      </article>

      <!-- Card: System Analysis & Design -->
      <article class="service-card">
        <div class="card-icon-wrap">
          <!-- Puzzle icon -->
          <svg width="28" height="28" viewBox="0 0 24 24" fill="#9eff00" aria-hidden="true">
            <path d="M20.5 11H19V7a2 2 0 0 0-2-2h-4V3.5a2.5 2.5 0 0 0-5 0V5H4a2 2 0 0 0-2 2v3.8h1.5a2.5 2.5 0 0 1 0 5H2V20a2 2 0 0 0 2 2h3.8v-1.5a2.5 2.5 0 0 1 5 0V22H17a2 2 0 0 0 2-2v-4h1.5a2.5 2.5 0 0 0 0-5z"/>
          </svg>
        </div>
        <h3 class="card-title">System Analysis &amp; Design (APS)</h3>
        <p class="card-desc">
          Menyusun pemodelan sistem rinci (Use Case, Activity, Sequence Diagram) untuk kebutuhan aplikasi skala UMKM hingga organisasi.
        </p>
        <a href="#contact" class="card-btn">Learn More</a>
      </article>

      <!-- Card: IoT & Embedded Systems -->
      <article class="service-card">
        <div class="card-icon-wrap">
          <!-- Lightning bolt icon -->
          <svg width="28" height="28" viewBox="0 0 24 24" fill="#9eff00" aria-hidden="true">
            <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
          </svg>
        </div>
        <h3 class="card-title">IoT &amp; Embedded Systems</h3>
        <p class="card-desc">
          Mengembangkan prototipe perangkat keras pintar (seperti smart lock ESP32) yang terintegrasi langsung dengan bot Telegram atau API web.
        </p>
        <a href="#contact" class="card-btn">Learn More</a>
      </article>

    </div>
  </section>
</template>

<script>
export default {
  mounted() {
    this.drawBannerMesh()
    window.addEventListener('resize', this.drawBannerMesh)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.drawBannerMesh)
  },
  methods: {
    drawBannerMesh() {
      const canvas = this.$el.querySelector('.banner-canvas')
      if (!canvas) return
      const ctx = canvas.getContext('2d')

      const W = canvas.offsetWidth  || 1200
      const H = canvas.offsetHeight || 280
      canvas.width  = W
      canvas.height = H

      const COLS = 70
      const ROWS = 28
      const cellW = W / COLS
      const cellH = H / ROWS

      // Build terrain heights — rolling hills / mountain silhouette
      const heights = []
      for (let r = 0; r <= ROWS; r++) {
        heights[r] = []
        for (let c = 0; c <= COLS; c++) {
          const nx = c / COLS
          const ny = r / ROWS
          const peak1 = Math.exp(-((nx - 0.3) ** 2 + (ny - 0.9) ** 2) * 14) * 160
          const peak2 = Math.exp(-((nx - 0.7) ** 2 + (ny - 0.9) ** 2) * 18) * 130
          const wave  = Math.sin(nx * Math.PI * 4) * 10 + Math.sin(ny * Math.PI * 3) * 6
          heights[r][c] = peak1 + peak2 + wave
        }
      }

      const fov   = 480
      const viewZ = -160

      const project = (x3, y3, z3) => {
        const scale = fov / (fov + z3 - viewZ)
        return {
          x: W / 2 + x3 * scale,
          y: H * 0.78 + y3 * scale,
        }
      }

      ctx.clearRect(0, 0, W, H)

      for (let r = 0; r < ROWS; r++) {
        for (let c = 0; c < COLS; c++) {
          const x3  = (c        - COLS / 2) * cellW * 0.88
          const z3  = (r        - ROWS * 0.05) * cellH * 1.05
          const y3  = -heights[r][c]

          const x3r = (c + 1    - COLS / 2) * cellW * 0.88
          const y3r = -heights[r][c + 1]

          const z3d = ((r + 1)  - ROWS * 0.05) * cellH * 1.05
          const y3d = -heights[r + 1][c]

          const p  = project(x3,  y3,  z3)
          const pr = project(x3r, y3r, z3)
          const pd = project(x3,  y3d, z3d)

          const depth = r / ROWS
          const alpha = 0.1 + (1 - depth) * 0.4
          ctx.strokeStyle = `rgba(158, 255, 0, ${alpha})`
          ctx.lineWidth   = depth < 0.25 ? 0.35 : 0.65

          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pr.x, pr.y); ctx.stroke()
          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pd.x, pd.y); ctx.stroke()
        }
      }

      // Bottom fade
      const grad = ctx.createLinearGradient(0, H * 0.5, 0, H)
      grad.addColorStop(0, 'rgba(15,15,15,0)')
      grad.addColorStop(1, 'rgba(15,15,15,1)')
      ctx.fillStyle = grad
      ctx.fillRect(0, H * 0.5, W, H * 0.5)

      // Top fade
      const gradTop = ctx.createLinearGradient(0, 0, 0, H * 0.35)
      gradTop.addColorStop(0, 'rgba(15,15,15,1)')
      gradTop.addColorStop(1, 'rgba(15,15,15,0)')
      ctx.fillStyle = gradTop
      ctx.fillRect(0, 0, W, H * 0.35)
    }
  }
}
</script>

<style scoped>
/* =========================================
   TOOLS STRIP
   ========================================= */
.tools-strip {
  width: 100%;
  background-color: #111111;
  border-top: 1px solid #1e1e1e;
  border-bottom: 1px solid #1e1e1e;
  padding: 2rem 0 2.2rem;
  overflow: hidden;
}

.tools-label {
  text-align: center;
  font-family: var(--font-main, sans-serif);
  font-size: 0.88rem;
  font-weight: 400;
  color: #6b6b6b;
  letter-spacing: 0.04em;
  margin-bottom: 1.6rem;
}

.tools-track-wrapper {
  width: 100%;
  overflow: hidden;
}

.tools-track {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4rem;
  flex-wrap: wrap;
  padding: 0 2rem;
}

.tool-item {
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0.85;
  transition: opacity 0.2s ease, transform 0.2s ease;
  cursor: default;
}

.tool-item:hover {
  opacity: 1;
  transform: translateY(-2px);
}

/* =========================================
   OUR SERVICES BANNER
   ========================================= */
.services-banner {
  position: relative;
  width: 100%;
  min-height: 280px;
  background-color: #0f0f0f;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.banner-canvas-wrapper {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.banner-canvas {
  width: 100%;
  height: 100%;
  display: block;
}

.banner-content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 3.5rem 2rem;
  max-width: 680px;
}

.banner-title {
  font-family: var(--font-main, sans-serif);
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  color: #ffffff;
  letter-spacing: -0.02em;
  margin-bottom: 1rem;
}

.banner-subtitle {
  font-family: var(--font-main, sans-serif);
  font-size: 0.97rem;
  font-weight: 400;
  color: #8a8a8a;
  line-height: 1.65;
  max-width: 560px;
  margin: 0 auto;
}

/* =========================================
   SERVICE CARDS GRID
   ========================================= */
.cards-section {
  width: 100%;
  background-color: #111111;
  padding: 3.5rem 2rem 4rem;
}

.cards-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

/* Individual Card */
.service-card {
  background-color: #151515;
  border: 1px solid #232323;
  border-radius: 12px;
  padding: 2rem 1.75rem 1.75rem;
  display: flex;
  flex-direction: column;
  gap: 0;
  transition: border-color 0.2s ease, transform 0.2s ease;
}

.service-card:hover {
  border-color: #333333;
  transform: translateY(-3px);
}

/* Icon wrapper */
.card-icon-wrap {
  width: 58px;
  height: 58px;
  background-color: #1c1c1c;
  border: 1px solid #2a2a2a;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.6rem;
  flex-shrink: 0;
}

/* Title */
.card-title {
  font-family: var(--font-main, sans-serif);
  font-size: 1.18rem;
  font-weight: 700;
  color: #f0f0f0;
  letter-spacing: -0.01em;
  line-height: 1.3;
  margin-bottom: 0.9rem;
}

/* Description */
.card-desc {
  font-family: var(--font-main, sans-serif);
  font-size: 0.9rem;
  font-weight: 400;
  color: #717171;
  line-height: 1.7;
  flex: 1;
  margin-bottom: 2rem;
}

/* Learn More button */
.card-btn {
  display: block;
  text-align: center;
  font-family: var(--font-main, sans-serif);
  font-size: 0.9rem;
  font-weight: 500;
  color: #c0c0c0;
  background-color: transparent;
  border: 1px solid #2a2a2a;
  border-radius: 8px;
  padding: 0.75rem 1rem;
  text-decoration: none;
  transition: all 0.2s ease;
  margin-top: auto;
}

.card-btn:hover {
  background-color: #1e1e1e;
  border-color: #444444;
  color: #ffffff;
}

/* =========================================
   RESPONSIVE
   ========================================= */
@media (max-width: 900px) {
  .cards-grid {
    grid-template-columns: 1fr;
    max-width: 480px;
  }
}

@media (max-width: 600px) {
  .tools-track {
    gap: 2.5rem;
  }

  .banner-title {
    font-size: 1.8rem;
  }

  .cards-section {
    padding: 2.5rem 1.25rem 3rem;
  }
}
</style>
