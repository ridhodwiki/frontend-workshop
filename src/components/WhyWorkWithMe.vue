<script setup>
const features = [
  {
    title: 'Systematic & Structured',
    icon: 'systematic',
    desc: 'Berpengalaman dalam memodelkan sistem secara rinci (Use Case, Activity, & Sequence Diagram) sehingga pengembangan perangkat lunak berjalan terstruktur, terarah, dan sesuai kebutuhan.'
  },
  {
    title: 'User-Centric Design',
    icon: 'usercentric',
    desc: 'Fokus merancang antarmuka (UI/UX) yang tidak hanya estetik dan modern, tetapi juga memberikan pengalaman pengguna yang mudah, responsif, dan fungsional.'
  },
  {
    title: 'Hardware & IoT Integration',
    icon: 'hardware',
    desc: 'Memiliki kapabilitas menggabungkan sistem embedded/IoT (seperti mikrokontroler ESP32) dengan platform komunikasi atau API web untuk solusi sistem pintar.'
  },
  {
    title: 'Analytical & Problem Solver',
    icon: 'analytical',
    desc: 'Mampu menganalisis permasalahan teknis dan kuantitatif secara mendalam untuk merumuskan solusi teknologi yang efisien dan tepat sasaran.'
  }
]
</script>

<template>
  <section id="work" class="work-section" aria-label="Why Work With Me">
    <div class="work-banner">
      <div class="banner-canvas-wrap" aria-hidden="true">
        <canvas ref="bannerCanvas" class="banner-canvas"></canvas>
      </div>
      <div class="banner-inner">
        <h2 class="banner-title">Why Work With Me?</h2>
        <p class="banner-sub">
          Mengintegrasikan desain UI/UX yang intuitif dengan analisis sistem terstruktur dan teknologi IoT modern untuk menghasilkan solusi digital yang solutif.
        </p>
      </div>
    </div>

    <div class="features-grid">
      <article v-for="f in features" :key="f.title" class="feature-card">
        <div class="feature-head">
          <div class="icon-box">
            <svg v-if="f.icon==='systematic'" width="22" height="22" viewBox="0 0 24 24" fill="#9EFF00" aria-hidden="true">
              <path d="M12 2l2.4 4.86 5.36.78-3.88 3.78.92 5.34L12 14.77l-4.8 2.52.92-5.34L4.24 7.64l5.36-.78L12 2zM12 18a3 3 0 100 6 3 3 0 000-6zm0 1.5l.9 1.82 2 .29-1.45 1.41.34 2-1.79-.94-1.79.94.34-2L9.1 20.79l2-.29L12 19.5z"/>
              <path d="M7 4l-1.5-2H5a1 1 0 00-.9 1.45L7 9l2-1-2-4zM17 4l2-4 2.5 2H21a1 1 0 01-.9 1.45L17 9l-2-1 2-4z" opacity=".9"/>
            </svg>
            <svg v-else-if="f.icon==='usercentric'" width="22" height="22" viewBox="0 0 24 24" fill="#9EFF00" aria-hidden="true">
              <circle cx="7" cy="8" r="3"/><path d="M2 18c0-2.21 2.69-4 6-4s6 1.79 6 4v2H2v-2z"/>
              <circle cx="16" cy="8" r="2.5"/><path d="M17.5 18v-1.2c0-1.3-.8-2.4-2-2.9.6-.3 1-.9 1-1.6" fill="none" stroke="#9EFF00" stroke-width="1.6" stroke-linecap="round"/>
              <path d="M19 6c1.1 0 2 .9 2 2s-.9 2-2 2" fill="none" stroke="#9EFF00" stroke-width="1.6" stroke-linecap="round"/>
              <path d="M19 9c.7 0 1.3.6 1.3 1.3S19.7 11.6 19 11.6" fill="none" stroke="#9EFF00" stroke-width="1.4" stroke-linecap="round"/>
            </svg>
            <svg v-else-if="f.icon==='hardware'" width="20" height="20" viewBox="0 0 24 24" fill="#9EFF00" aria-hidden="true">
              <path d="M13 2L3 14h8l-1 8 11-12h-8l1-8z"/>
            </svg>
            <svg v-else width="22" height="22" viewBox="0 0 24 24" fill="#9EFF00" aria-hidden="true">
              <path d="M3 16l-1-5 4 2 4-7 4 7 4-2-1 5H3z"/><path d="M5 19h14v2H5z"/>
            </svg>
          </div>
          <h3 class="feature-title">{{ f.title }}</h3>
        </div>
        <p class="feature-desc">{{ f.desc }}</p>
      </article>
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
      const W = canvas.offsetWidth || 1200
      const H = canvas.offsetHeight || 300
      canvas.width = W
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
          const peak2 = Math.exp(-((nx - 0.72) ** 2 + (ny - 0.9) ** 2) * 16) * 120
          const wave = Math.sin(nx * Math.PI * 3.5) * 9 + Math.sin(ny * Math.PI * 2.5) * 5
          heights[r][c] = peak1 + peak2 + wave
        }
      }

      const fov = 480
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
          const x3 = (c - COLS / 2) * cellW * 0.88
          const z3 = (r - ROWS * 0.05) * cellH * 1.05
          const y3 = -heights[r][c]
          const x3r = (c + 1 - COLS / 2) * cellW * 0.88
          const y3r = -heights[r][c + 1]
          const z3d = (r + 1 - ROWS * 0.05) * cellH * 1.05
          const y3d = -heights[r + 1][c]
          const p = project(x3, y3, z3)
          const pr = project(x3r, y3r, z3)
          const pd = project(x3, y3d, z3d)
          const depth = r / ROWS
          const alpha = 0.08 + (1 - depth) * 0.32
          ctx.strokeStyle = `rgba(158,255,0,${alpha})`
          ctx.lineWidth = depth < 0.25 ? 0.35 : 0.6
          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pr.x, pr.y); ctx.stroke()
          ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(pd.x, pd.y); ctx.stroke()
        }
      }

      const gBot = ctx.createLinearGradient(0, H * 0.45, 0, H)
      gBot.addColorStop(0, 'rgba(10,10,10,0)')
      gBot.addColorStop(1, 'rgba(10,10,10,1)')
      ctx.fillStyle = gBot
      ctx.fillRect(0, H * 0.45, W, H * 0.55)

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
.work-section {
  width: 100%;
  background: #111111;
  border-top: 1px solid #1e1e1e;
}
.work-banner {
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
.work-banner::after {
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
.features-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  background: #1e1e1e;
  gap: 1px;
  border-top: 1px solid #1e1e1e;
  border-bottom: 1px solid #1e1e1e;
}
.feature-card {
  background: #151515;
  padding: 2.2rem 2rem 2.4rem;
  display: flex;
  flex-direction: column;
  gap: 1.15rem;
}
.feature-head {
  display: flex;
  align-items: center;
  gap: 0.9rem;
}
.icon-box {
  width: 44px;
  height: 44px;
  flex-shrink: 0;
  border-radius: 8px;
  background: linear-gradient(135deg, #1e2a08 0%, #1a1a1a 65%);
  border: 1px solid #252525;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: inset 0 1px 0 rgba(158,255,0,0.08);
}
.feature-title {
  font-family: var(--font-main, sans-serif);
  font-size: 0.98rem;
  font-weight: 600;
  color: #ececec;
  letter-spacing: -0.01em;
  line-height: 1.3;
}
.feature-desc {
  font-family: var(--font-main, sans-serif);
  font-size: 0.84rem;
  font-weight: 400;
  color: #7a7a7a;
  line-height: 1.75;
}
@media (max-width: 720px) {
  .features-grid { grid-template-columns: 1fr; }
  .feature-card { padding: 1.9rem 1.35rem 2rem; }
  .work-banner { min-height: 220px; }
  .banner-sub { font-size: 0.78rem; }
}
</style>
