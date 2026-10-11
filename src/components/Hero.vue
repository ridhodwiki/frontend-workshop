<script setup>
// Hero section - Informatics Student & Tech Craftsman
const tags = ['UI / UX Design', 'System Analysis', 'Web Dev', 'IoT']
</script>

<template>
  <section id="home" class="hero-section">
    <!-- Background wireframe mesh canvas -->
    <div class="hero-canvas">
      <canvas ref="meshCanvas" class="mesh-canvas" aria-hidden="true"></canvas>
    </div>

    <!-- Hero Content -->
    <div class="hero-content">
      <!-- Main Heading -->
      <h1 class="hero-title">
        Informatics Student &amp; Tech Craftsman Building Digital Solutions
      </h1>

      <!-- Tag Pills Row -->
      <div class="hero-tags" aria-label="Specialization areas">
        <span class="tag-label">For</span>
        <template v-for="(tag, index) in tags" :key="tag">
          <span class="tag-pill">{{ tag }}</span>
          <span v-if="index < tags.length - 2" class="tag-separator">,</span>
          <span v-else-if="index === tags.length - 2" class="tag-separator">and</span>
        </template>
      </div>

      <!-- CTA Buttons -->
      <div class="hero-actions">
        <a href="#work" class="btn-outline">Explore Works</a>
        <a href="#contact" class="btn-lime">Contact Us</a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  mounted() {
    this.initMesh()
    window.addEventListener('resize', this.initMesh)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.initMesh)
    if (this.animFrameId) cancelAnimationFrame(this.animFrameId)
  },
  methods: {
    initMesh() {
      const canvas = this.$el.querySelector('.mesh-canvas')
      if (!canvas) return
      const ctx = canvas.getContext('2d')

      const W = canvas.offsetWidth
      const H = canvas.offsetHeight
      canvas.width = W
      canvas.height = H

      // Grid configuration
      const COLS = 60
      const ROWS = 30
      const cellW = W / COLS
      const cellH = H / ROWS

      // Perspective projection helpers
      const fov = 500
      const viewZ = -200

      // Generate terrain heights using sum of sine waves (mountain-like)
      const heights = []
      for (let r = 0; r <= ROWS; r++) {
        heights[r] = []
        for (let c = 0; c <= COLS; c++) {
          const nx = c / COLS
          const ny = r / ROWS
          // Two mountain peaks
          const peak1 = Math.exp(-((nx - 0.35) ** 2 + (ny - 0.7) ** 2) * 18) * 220
          const peak2 = Math.exp(-((nx - 0.65) ** 2 + (ny - 0.7) ** 2) * 22) * 180
          const base = Math.sin(nx * Math.PI * 3) * 12 + Math.sin(ny * Math.PI * 2) * 8
          heights[r][c] = peak1 + peak2 + base
        }
      }

      const project = (x3d, y3d, z3d) => {
        const scale = fov / (fov + z3d - viewZ)
        return {
          x: W / 2 + x3d * scale,
          y: H * 0.72 + y3d * scale,
          s: scale
        }
      }

      const draw = () => {
        ctx.clearRect(0, 0, W, H)

        const lineColor = 'rgba(158, 255, 0, 0.55)'
        const lineColorFar = 'rgba(158, 255, 0, 0.12)'

        for (let r = 0; r < ROWS; r++) {
          for (let c = 0; c < COLS; c++) {
            const x3d = (c - COLS / 2) * cellW * 0.9
            const z3d = (r - ROWS * 0.1) * cellH * 1.1
            const y3d = -heights[r][c]

            const x3d_r = ((c + 1) - COLS / 2) * cellW * 0.9
            const z3d_r = z3d
            const y3d_r = -heights[r][c + 1]

            const x3d_d = x3d
            const z3d_d = ((r + 1) - ROWS * 0.1) * cellH * 1.1
            const y3d_d = -heights[r + 1][c]

            const p  = project(x3d,   y3d,   z3d)
            const pr = project(x3d_r, y3d_r, z3d_r)
            const pd = project(x3d_d, y3d_d, z3d_d)

            // Fade lines based on depth (far rows more transparent)
            const depthRatio = r / ROWS
            const alpha = 0.12 + (1 - depthRatio) * 0.43
            ctx.strokeStyle = `rgba(158, 255, 0, ${alpha})`
            ctx.lineWidth = depthRatio < 0.3 ? 0.4 : 0.75

            // Horizontal line
            ctx.beginPath()
            ctx.moveTo(p.x, p.y)
            ctx.lineTo(pr.x, pr.y)
            ctx.stroke()

            // Vertical line
            ctx.beginPath()
            ctx.moveTo(p.x, p.y)
            ctx.lineTo(pd.x, pd.y)
            ctx.stroke()
          }
        }

        // Bottom fade gradient overlay
        const grad = ctx.createLinearGradient(0, H * 0.55, 0, H)
        grad.addColorStop(0, 'rgba(18, 18, 18, 0)')
        grad.addColorStop(1, 'rgba(18, 18, 18, 1)')
        ctx.fillStyle = grad
        ctx.fillRect(0, H * 0.55, W, H * 0.45)
      }

      draw()
    }
  }
}
</script>

<style scoped>
/* =========================================
   HERO SECTION
   ========================================= */
.hero-section {
  position: relative;
  width: 100%;
  min-height: calc(100vh - var(--header-height, 84px));
  background-color: #121212;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  overflow: hidden;
}

/* Canvas covers the bottom half of the hero */
.hero-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.mesh-canvas {
  width: 100%;
  height: 100%;
  display: block;
}

/* =========================================
   HERO CONTENT (CENTERED)
   ========================================= */
.hero-content {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 1100px;
  padding: 0 2rem;
  margin-top: clamp(80px, 12vh, 140px);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  text-align: center;
}

/* =========================================
   MAIN HEADING
   ========================================= */
.hero-title {
  font-family: var(--font-main, 'Plus Jakarta Sans', sans-serif);
  font-size: clamp(2.4rem, 5.5vw, 4.2rem);
  font-weight: 700;
  line-height: 1.13;
  letter-spacing: -0.03em;
  color: #ffffff;
  max-width: 860px;
}

/* =========================================
   TAG PILLS ROW
   ========================================= */
.hero-tags {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.45rem 0.6rem;
  font-family: var(--font-main, sans-serif);
  font-size: 0.95rem;
  color: #c0c0c0;
}

.tag-label {
  color: #8a8a8a;
  font-weight: 400;
}

.tag-separator {
  color: #8a8a8a;
  font-weight: 400;
}

.tag-pill {
  display: inline-flex;
  align-items: center;
  padding: 0.38rem 0.9rem;
  background-color: #1e1e1e;
  border: 1px solid #2e2e2e;
  border-radius: 6px;
  color: #e0e0e0;
  font-size: 0.92rem;
  font-weight: 500;
  letter-spacing: 0.01em;
}

/* =========================================
   CTA BUTTONS
   ========================================= */
.hero-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 0.5rem;
}

/* Outline button (Explore Works) */
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

/* Lime/neon button (Contact Us) */
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

/* =========================================
   RESPONSIVE
   ========================================= */
@media (max-width: 768px) {
  .hero-title {
    font-size: clamp(1.9rem, 7vw, 2.6rem);
  }

  .hero-content {
    margin-top: 60px;
    gap: 1.6rem;
  }

  .hero-tags {
    font-size: 0.88rem;
  }

  .tag-pill {
    font-size: 0.85rem;
    padding: 0.32rem 0.75rem;
  }
}

@media (max-width: 480px) {
  .btn-outline,
  .btn-lime {
    width: 100%;
    max-width: 280px;
  }
}
</style>
