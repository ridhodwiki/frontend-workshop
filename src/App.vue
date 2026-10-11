<script setup>
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Services from './components/Services.vue'
import WhyWorkWithMe from './components/WhyWorkWithMe.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="app-container">
    <!-- Sticky Header -->
    <Header />

    <main>
      <!-- Hero Section -->
      <Hero />

      <!-- Services Section -->
      <Services />

      <!-- Why Work With Me -->
      <WhyWorkWithMe />

      <!-- About Me -->
      <About />

      <!-- Contact -->
      <Contact />
    </main>

    <!-- Footer -->
    <Footer />
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  position: relative;
  background-color: var(--color-bg-primary);
}
</style>
