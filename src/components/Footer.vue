<script setup>
const navLinks = [
  { label: 'Home',     href: '#home'    },
  { label: 'Services', href: '#services' },
  { label: 'Work',     href: '#work'    },
  { label: 'About',    href: '#about'   },
  { label: 'Contact',  href: '#contact' },
]

const year = new Date().getFullYear()
</script>

<template>
  <footer class="site-footer" aria-label="Site Footer">

    <!-- =============================================
         FOOTER MAIN — logo + nav + social
         ============================================= -->
    <div class="footer-main">
      <div class="footer-inner">

        <!-- Logo -->
        <div class="footer-brand">
          <div class="brand-icon" aria-hidden="true">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="#9EFF00" aria-hidden="true">
              <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
            </svg>
          </div>
          <span class="brand-name">Ridho Dwiki</span>
        </div>

        <!-- Nav links -->
        <nav class="footer-nav" aria-label="Footer navigation">
          <a
            v-for="link in navLinks"
            :key="link.label"
            :href="link.href"
            class="footer-nav-link"
          >{{ link.label }}</a>
        </nav>

        <!-- Stay Connected + social icons -->
        <div class="footer-social">
          <span class="social-label">Stay Connected</span>
          <div class="social-icons" role="list">
            <a
              href="https://facebook.com/"
              target="_blank"
              rel="noopener noreferrer"
              class="social-icon-btn"
              aria-label="Facebook"
              role="listitem"
            >
              <svg width="17" height="17" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>
              </svg>
            </a>
            <a
              href="https://twitter.com/"
              target="_blank"
              rel="noopener noreferrer"
              class="social-icon-btn"
              aria-label="Twitter / X"
              role="listitem"
            >
              <svg width="17" height="17" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M22 4s-.7 2.1-2 3.4c1.6 10-9.4 17.3-18 11.6 2.2.1 4.4-.6 6-2C3 15.5.5 9.6 3 5c2.2 2.6 5.6 4.1 9 4-.9-4.2 4-6.6 7-3.8 1.1 0 3-1.2 3-1.2z"/>
              </svg>
            </a>
            <a
              href="https://linkedin.com/"
              target="_blank"
              rel="noopener noreferrer"
              class="social-icon-btn"
              aria-label="LinkedIn"
              role="listitem"
            >
              <svg width="17" height="17" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
              </svg>
            </a>
          </div>
        </div>

      </div>
    </div>

    <!-- =============================================
         FOOTER BOTTOM — contact info + copyright
         ============================================= -->
    <div class="footer-bottom">
      <div class="footer-inner footer-bottom-inner">

        <!-- Contact quick info -->
        <div class="footer-contacts">
          <a href="mailto:ridhodwiki768@gmail.com" class="footer-contact-item" aria-label="Email">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
              <rect x="2" y="4" width="20" height="16" rx="2"/>
              <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
            </svg>
            <span>ridhodwiki768@gmail.com</span>
          </a>

          <a href="tel:+62895263521118" class="footer-contact-item" aria-label="Phone">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
              <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.6 1.27h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L7.91 8.9a16 16 0 0 0 6 6l.96-.96a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/>
            </svg>
            <span>+62 895 2635 2118</span>
          </a>

          <div class="footer-contact-item no-link" aria-label="Location">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
              <path d="M20 10c0 6-8 12-8 12S4 16 4 10a8 8 0 1 1 16 0z"/>
              <circle cx="12" cy="10" r="3"/>
            </svg>
            <span>Pemalang, Indonesia</span>
          </div>
        </div>

        <!-- Copyright -->
        <p class="footer-copy">
          © {{ year }} Ridho Dwiki. All rights reserved.
        </p>

      </div>
    </div>

  </footer>
</template>

<style scoped>
/* =========================================
   FOOTER
   ========================================= */
.site-footer {
  width: 100%;
  background: #0d0d0d;
  border-top: 1px solid #1e1e1e;
}

/* =========================================
   SHARED INNER WIDTH — 1200px (sama dengan section lain)
   ========================================= */
.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

/* =========================================
   FOOTER MAIN
   ========================================= */
.footer-main {
  border-bottom: 1px solid #1a1a1a;
  padding: 1.8rem 0;
}

.footer-main .footer-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;
  flex-wrap: wrap;
}

/* Brand / Logo */
.footer-brand {
  display: flex;
  align-items: center;
  gap: 0.65rem;
  text-decoration: none;
  flex-shrink: 0;
}

.brand-icon {
  width: 38px;
  height: 38px;
  background: #1a2208;
  border: 1px solid #2c3d0a;
  border-radius: 9px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 12px rgba(158,255,0,0.1);
}

.brand-name {
  font-family: var(--font-main, sans-serif);
  font-size: 1rem;
  font-weight: 700;
  color: #f0f0f0;
  letter-spacing: -0.01em;
}

/* Nav */
.footer-nav {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  flex-wrap: wrap;
}

.footer-nav-link {
  font-family: var(--font-main, sans-serif);
  font-size: 0.88rem;
  font-weight: 400;
  color: #888;
  text-decoration: none;
  padding: 0.35rem 0.75rem;
  border-radius: 5px;
  transition: color 0.2s, background 0.2s;
}

.footer-nav-link:hover {
  color: #e0e0e0;
  background: #1a1a1a;
}

/* Social */
.footer-social {
  display: flex;
  align-items: center;
  gap: 0.9rem;
  flex-shrink: 0;
}

.social-label {
  font-family: var(--font-main, sans-serif);
  font-size: 0.82rem;
  font-weight: 400;
  color: #555;
}

.social-icons {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.social-icon-btn {
  width: 34px;
  height: 34px;
  background: #171717;
  border: 1px solid #242424;
  border-radius: 7px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #666;
  text-decoration: none;
  transition: color 0.2s, border-color 0.2s, background 0.2s;
}

.social-icon-btn:hover {
  color: #9EFF00;
  border-color: #9EFF00;
  background: #1a2208;
}

/* =========================================
   FOOTER BOTTOM
   ========================================= */
.footer-bottom {
  padding: 1.2rem 0;
}

.footer-bottom-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.footer-contacts {
  display: flex;
  align-items: center;
  gap: 1.75rem;
  flex-wrap: wrap;
}

.footer-contact-item {
  display: flex;
  align-items: center;
  gap: 0.45rem;
  font-family: var(--font-main, sans-serif);
  font-size: 0.78rem;
  font-weight: 400;
  color: #555;
  text-decoration: none;
  transition: color 0.2s;
}

.footer-contact-item:not(.no-link):hover {
  color: #9EFF00;
}

.footer-contact-item.no-link {
  cursor: default;
}

.footer-contact-item span {
  white-space: nowrap;
}

.footer-copy {
  font-family: var(--font-main, sans-serif);
  font-size: 0.78rem;
  font-weight: 400;
  color: #3d3d3d;
  white-space: nowrap;
}

/* =========================================
   RESPONSIVE
   ========================================= */
@media (max-width: 900px) {
  .footer-main .footer-inner {
    flex-direction: column;
    align-items: flex-start;
    gap: 1.4rem;
  }

  .footer-social {
    align-self: flex-start;
  }
}

@media (max-width: 640px) {
  .footer-bottom-inner {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }

  .footer-contacts {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.65rem;
  }

  .footer-nav {
    gap: 0.1rem;
  }

  .footer-inner {
    padding: 0 1.25rem;
  }
}
</style>
