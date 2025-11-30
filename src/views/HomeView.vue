<script setup>
import { ref, onMounted } from 'vue'
import HeroSection from '../components/HeroSection.vue'
import AboutSection from '../components/AboutSection.vue'
import SkillsSection from '../components/SkillsSection.vue'
import ProjectsSection from '../components/ProjectsSection.vue'
import ContactSection from '../components/ContactSection.vue'
import NavBar from '../components/NavBar.vue'

const isLoaded = ref(false)

onMounted(() => {
  setTimeout(() => {
    isLoaded.value = true
  }, 100)
})
</script>

<template>
  <div class="portfolio" :class="{ loaded: isLoaded }">
    <NavBar />
    <main>
      <HeroSection />
      <AboutSection />
      <SkillsSection />
      <ProjectsSection />
      <ContactSection />
    </main>
    <footer class="footer">
      <p>© 2025 Kim Kangyeon. All rights reserved.</p>
    </footer>
  </div>
</template>

<style scoped>
.portfolio {
  opacity: 0;
  transition: opacity 0.6s ease;
}

.portfolio.loaded {
  opacity: 1;
}

main {
  overflow-x: hidden;
}

.footer {
  text-align: center;
  padding: 2rem;
  border-top: 1px solid var(--border-color);
  color: var(--text-secondary);
  font-size: 0.875rem;
}
</style>
