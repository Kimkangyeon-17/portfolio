<script setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { projects } from '../data/projects'

const route = useRoute()
const router = useRouter()

const project = computed(() => {
  return projects.find((p) => p.id === Number(route.params.id))
})

const goBack = () => {
  router.push('/#projects')
}
</script>

<template>
  <div class="project-detail" v-if="project">
    <div class="container">
      <button @click="goBack" class="back-btn">← Back to Projects</button>
      
      <div class="header">
        <h1 class="title">{{ project.title }}</h1>
        <p class="subtitle">{{ project.subtitle }}</p>
      </div>

      <div class="content">
        <div class="description-section">
          <h2>Project Overview</h2>
          <p class="description">{{ project.description }}</p>
          
          <div class="links" v-if="project.github">
             <a :href="project.github" target="_blank" rel="noopener" class="github-link">
               Visit GitHub Repository
             </a>
          </div>
        </div>

        <div class="features-section">
          <h2>Key Features</h2>
          <ul class="features-list">
            <li v-for="feature in project.features" :key="feature">
              {{ feature }}
            </li>
          </ul>
        </div>

        <div class="tech-section">
          <h2>Tech Stack</h2>
          <div class="tech-tags">
            <span v-for="tech in project.tech" :key="tech" class="tech-tag">
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="not-found">
    <p>Project not found.</p>
    <button @click="goBack">Go Back</button>
  </div>
</template>

<style scoped>
.project-detail {
  min-height: 100vh;
  padding: 8rem 2rem;
  background: var(--bg-primary);
  color: var(--text-primary);
}

.container {
  max-width: 800px;
  margin: 0 auto;
}

.back-btn {
  background: none;
  border: none;
  color: var(--text-secondary);
  font-family: 'JetBrains Mono', monospace;
  cursor: pointer;
  margin-bottom: 2rem;
  font-size: 1rem;
  transition: color 0.3s;
}

.back-btn:hover {
  color: var(--accent-primary);
}

.header {
  margin-bottom: 4rem;
}

.title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  background: var(--accent-gradient);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.subtitle {
  font-size: 1.25rem;
  color: var(--text-secondary);
}

.content {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: var(--text-primary);
  border-left: 3px solid var(--accent-primary);
  padding-left: 1rem;
}

.description {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--text-secondary);
  margin-bottom: 2rem;
}

.github-link {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  color: var(--text-primary);
  text-decoration: none;
  border-radius: 8px;
  transition: all 0.3s;
}

.github-link:hover {
  border-color: var(--accent-primary);
  transform: translateY(-2px);
}

.features-list {
  list-style: none;
  display: grid;
  gap: 1rem;
}

.features-list li {
  padding: 1rem;
  background: var(--bg-card);
  border-radius: 8px;
  border: 1px solid var(--border-color);
  color: var(--text-secondary);
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.tech-tag {
  background: var(--bg-card);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  border: 1px solid var(--border-color);
  color: var(--accent-secondary);
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.9rem;
}

.not-found {
  padding: 10rem 0;
  text-align: center;
}
</style>
