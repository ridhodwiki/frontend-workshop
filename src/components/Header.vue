<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)
const activeMenu = ref('Home')

// 4 Menu Navigasi persis seperti pada gambar: Home, Services, Work, About
const navItems = [
  { name: 'Home', href: '#home' },
  { name: 'Services', href: '#services' },
  { name: 'Work', href: '#work' },
  { name: 'About', href: '#about' }
]

const handleScroll = () => {
  if (window.scrollY > 15) {
    isScrolled.value = true
  } else {
    isScrolled.value = false
  }
}

const handleNavClick = (item) => {
  activeMenu.value = item.name
  isMobileMenuOpen.value = false

  const target = document.querySelector(item.href)
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' })
  }
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header
    :class="['header-container', { 'is-scrolled': isScrolled, 'menu-opened': isMobileMenuOpen }]"
  >
    <div class="header-inner">
      <!-- Sisi Kiri: Logo Ridho Dwiki dengan Icon Isometric Cube Khas SquareUp -->
      <a href="#home" class="brand-logo" @click.prevent="handleNavClick({ name: 'Home', href: '#home' })">
        <div class="logo-box">
          <svg width="40" height="40" viewBox="0 0 41 40" fill="none" xmlns="http://www.w3.org/2000/svg" class="logo-svg">
            <rect width="40" height="40" rx="7" fill="#9EFF00"/>
            <path d="M7.32422 12.4749L20.0942 20V34.3662L7.32422 27.0691L7.32422 12.4749Z" fill="#111111"/>
            <path fill-rule="evenodd" clip-rule="evenodd" d="M21.2209 19.9899V32.4246L31.7374 26.4152V13.7927L21.2209 19.9899ZM32.8641 27.0691L20.0942 34.3662V20L7.32422 12.4748L20.0942 5.63379L32.8641 12.4748V27.0691ZM31.1466 12.833L20.0942 6.91205L9.62298 12.5216L20.649 19.0191L31.1466 12.833Z" fill="#111111"/>
          </svg>
        </div>
        <span class="brand-name">Ridho Dwiki</span>
      </a>

      <!-- Sisi Tengah: 4 Menu (Home, Services, Work, About) dengan Active Pill -->
      <nav class="desktop-nav" aria-label="Main Navigation">
        <ul class="nav-list">
          <li v-for="item in navItems" :key="item.name">
            <a
              :href="item.href"
              :class="['nav-link', { 'active': activeMenu === item.name }]"
              @click.prevent="handleNavClick(item)"
            >
              {{ item.name }}
            </a>
          </li>
        </ul>
      </nav>

      <!-- Sisi Kanan: Contact Us Button & Mobile Hamburger -->
      <div class="header-actions">
        <!-- Tombol Contact Us Neon Lime (#9EFF00) -->
        <a
          href="#contact"
          class="contact-btn"
          @click.prevent="handleNavClick({ name: 'Contact', href: '#contact' })"
        >
          Contact Us
        </a>

        <!-- Hamburger Button untuk Layar Tablet/Mobile -->
        <button
          class="mobile-toggle-btn"
          @click="toggleMobileMenu"
          :aria-expanded="isMobileMenuOpen"
          aria-label="Toggle navigation menu"
        >
          <svg v-if="!isMobileMenuOpen" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="3" y1="12" x2="21" y2="12"></line>
            <line x1="3" y1="6" x2="21" y2="6"></line>
            <line x1="3" y1="18" x2="21" y2="18"></line>
          </svg>
          <svg v-else width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>
      </div>
    </div>

    <!-- Dropdown Navigasi Mobile -->
    <transition name="drawer-slide">
      <div v-if="isMobileMenuOpen" class="mobile-drawer">
        <ul class="mobile-nav-list">
          <li v-for="item in navItems" :key="item.name">
            <a
              :href="item.href"
              :class="['mobile-nav-link', { 'active': activeMenu === item.name }]"
              @click.prevent="handleNavClick(item)"
            >
              {{ item.name }}
            </a>
          </li>
        </ul>
        <div class="mobile-drawer-cta">
          <a
            href="#contact"
            class="mobile-contact-btn"
            @click.prevent="handleNavClick({ name: 'Contact', href: '#contact' })"
          >
            Contact Us
          </a>
        </div>
      </div>
    </transition>
  </header>
</template>

<style scoped>
/* Header Sticky Wrapper */
.header-container {
  position: sticky;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 50;
  background-color: #121212;
  border-bottom: 1px solid #1f1f1f;
  transition: all 0.25s ease;
}

/* Keadaan Saat Di-scroll: Sedikit translucent dengan glass blur */
.header-container.is-scrolled {
  background-color: rgba(18, 18, 18, 0.92);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid #282828;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.45);
}

/* Inner Layout Shell */
.header-inner {
  max-width: 1540px;
  margin: 0 auto;
  padding: 1.25rem 3.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
}

/* =========================================
   LOGO (KIRI)
   ========================================= */
.brand-logo {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  text-decoration: none;
  cursor: pointer;
}

.logo-box {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.25s ease;
}

.brand-logo:hover .logo-box {
  transform: scale(1.05);
}

.logo-svg {
  width: 40px;
  height: 40px;
  display: block;
}

.brand-name {
  font-family: var(--font-main);
  font-size: 1.3rem;
  font-weight: 500;
  color: #ffffff;
  letter-spacing: -0.2px;
}

/* =========================================
   MENU NAVIGASI (TENGAH)
   ========================================= */
.desktop-nav {
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-list {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-main);
  font-size: 0.95rem;
  font-weight: 400;
  color: #d1d1d1;
  text-decoration: none;
  padding: 0.55rem 0.85rem;
  border-radius: 6px;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

.nav-link:hover {
  color: #ffffff;
}

/* Active Pill Sesuai Gambar Referensi */
.nav-link.active {
  background-color: #242424;
  color: #ffffff;
  font-weight: 500;
  padding: 0.55rem 1.25rem;
}

/* =========================================
   ACTIONS (KANAN)
   ========================================= */
.header-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

/* Tombol Contact Us Neon Lime (#9EFF00) */
.contact-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-main);
  font-size: 0.925rem;
  font-weight: 600;
  color: #111111;
  background-color: #9eff00;
  padding: 0.65rem 1.45rem;
  border-radius: 7px;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 2px 10px rgba(158, 255, 0, 0.15);
}

.contact-btn:hover {
  background-color: #acff24;
  transform: translateY(-1px);
  box-shadow: 0 4px 16px rgba(158, 255, 0, 0.3);
}

/* Mobile Toggle Hamburger Button */
.mobile-toggle-btn {
  display: none;
  align-items: center;
  justify-content: center;
  width: 42px;
  height: 42px;
  background-color: #242424;
  border: 1px solid #333333;
  border-radius: 6px;
  color: #ffffff;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.mobile-toggle-btn:hover {
  background-color: #2e2e2e;
}

/* =========================================
   MOBILE DRAWER NAVIGATION
   ========================================= */
.mobile-drawer {
  display: none;
}

/* Responsive Breakpoints */
@media (max-width: 900px) {
  .header-inner {
    padding: 1.15rem 1.5rem;
  }

  .desktop-nav {
    display: none;
  }

  .contact-btn {
    display: none;
  }

  .mobile-toggle-btn {
    display: flex;
  }

  .mobile-drawer {
    display: block;
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: #121212;
    border-bottom: 1px solid #1f1f1f;
    padding: 1.25rem 1.5rem 1.75rem;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.6);
  }

  .mobile-nav-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin-bottom: 1.25rem;
  }

  .mobile-nav-link {
    display: block;
    font-family: var(--font-main);
    padding: 0.75rem 1rem;
    font-size: 0.95rem;
    font-weight: 400;
    color: #b5b5b5;
    border-radius: 6px;
    text-decoration: none;
    transition: all 0.2s ease;
  }

  .mobile-nav-link:hover,
  .mobile-nav-link.active {
    background-color: #242424;
    color: #ffffff;
    font-weight: 500;
  }

  .mobile-drawer-cta {
    padding-top: 0.75rem;
    border-top: 1px solid #1f1f1f;
  }

  .mobile-contact-btn {
    display: block;
    text-align: center;
    font-family: var(--font-main);
    font-size: 0.95rem;
    font-weight: 600;
    color: #111111;
    background-color: #9eff00;
    padding: 0.8rem;
    border-radius: 6px;
    text-decoration: none;
  }

  .mobile-contact-btn:hover {
    background-color: #acff24;
  }

  /* Transition Animation */
  .drawer-slide-enter-active,
  .drawer-slide-leave-active {
    transition: opacity 0.25s ease, transform 0.25s ease;
  }

  .drawer-slide-enter-from,
  .drawer-slide-leave-to {
    opacity: 0;
    transform: translateY(-8px);
  }
}
</style>
