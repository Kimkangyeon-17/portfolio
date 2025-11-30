<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const projects = [
  {
    id: 1,
    title: 'DevRunDev',
    subtitle: 'IT 개발자를 위한 온라인 교육 플랫폼',
    description: '강사들은 실무 중심의 강의를 제작하고 수강생들은 최신 기술을 배우며 성장할 수 있도록 지원합니다. 강의 진행률, 평가 시스템, 강의 별 퀴즈 등의 기능을 통해 효율적인 학습 경험을 제공합니다.',
    features: [
      '역할 기반 사용자 시스템 (학생/강사/관리자)',
      '소셜 로그인 (Google, Kakao, Naver)',
      '강의 생성 및 승인 워크플로우',
      '강의 진행률 추적 및 수료증 발급',
      '퀴즈 시스템 및 리뷰 기능'
    ],
    tech: ['Django', 'SQLite', 'Bootstrap', 'JavaScript', 'HTML/CSS'],
    github: 'https://github.com/Kimkangyeon-17/DevRunDev',
    color: '#22c55e'
  },
  {
    id: 2,
    title: 'DevRunDev DRF',
    subtitle: 'REST API 기반 온라인 교육 플랫폼',
    description: 'DevRunDev의 REST API 버전으로, Django REST Framework를 활용하여 백엔드 API를 구축했습니다. 결제 시스템, QnA 기능, 관리자 대시보드 등 더욱 확장된 기능을 제공합니다.',
    features: [
      'RESTful API 설계 및 구현',
      'JWT/Token 기반 인증 시스템',
      '결제 시스템 통합',
      '레슨별 QnA 기능',
      '관리자 대시보드 및 분석'
    ],
    tech: ['Django', 'DRF', 'SQLite', 'HTMX', 'JavaScript', 'CSS'],
    github: 'https://github.com/Kimkangyeon-17/DevRunDev-DRF',
    color: '#6366f1'
  },
  {
    id: 3,
    title: 'Coming Soon',
    subtitle: '새로운 프로젝트 준비 중',
    description: '더 나은 서비스와 기술 역량 향상을 위해 새로운 프로젝트를 준비하고 있습니다. 곧 업데이트될 예정이니 기대해 주세요!',
    features: [],
    tech: ['TBD'],
    github: null,
    color: '#8b5cf6',
    isComingSoon: true
  }
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
        }
      })
    },
    { threshold: 0.1 }
  )

  const section = document.querySelector('#projects')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="projects" class="projects">
    <div class="container" :class="{ visible: isVisible }">
      <div class="section-header">
        <span class="section-number">03</span>
        <h2 class="section-title">Projects</h2>
        <div class="section-line"></div>
      </div>

      <div class="projects-grid">
        <article 
          v-for="(project, index) in projects" 
          :key="project.id" 
          class="project-card"
          :class="{ 'coming-soon': project.isComingSoon }"
          :style="{ '--delay': index * 0.15 + 's', '--accent': project.color }"
        >
          <div class="project-header">
            <div class="project-icon">
              <span v-if="!project.isComingSoon">📁</span>
              <span v-else>🚀</span>
            </div>
            <div class="project-links" v-if="project.github">
              <a :href="project.github" target="_blank" rel="noopener" class="project-link" title="GitHub">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                </svg>
              </a>
            </div>
          </div>

          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-subtitle">{{ project.subtitle }}</p>
            <p class="project-description">{{ project.description }}</p>

            <ul class="project-features" v-if="project.features.length">
              <li v-for="feature in project.features" :key="feature">
                {{ feature }}
              </li>
            </ul>
          </div>

          <div class="project-footer">
            <div class="project-tech">
              <span v-for="tech in project.tech" :key="tech" class="tech-tag">
                {{ tech }}
              </span>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects {
  padding: 8rem 2rem;
  background: var(--bg-secondary);
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.container.visible {
  opacity: 1;
  transform: translateY(0);
}

.section-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 3rem;
}

.section-number {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.875rem;
  color: var(--accent-primary);
}

.section-title {
  font-size: 2rem;
  font-weight: 700;
}

.section-line {
  flex: 1;
  height: 1px;
  background: var(--border-color);
  max-width: 300px;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
  gap: 1.5rem;
}

.project-card {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: 16px;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  transition: all 0.3s ease;
  animation: fadeInUp 0.6s ease forwards;
  animation-delay: var(--delay);
  opacity: 0;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.project-card:hover {
  border-color: var(--accent);
  transform: translateY(-4px);
}

.project-card.coming-soon {
  opacity: 0.7;
  border-style: dashed;
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.project-icon {
  font-size: 2.5rem;
}

.project-links {
  display: flex;
  gap: 0.75rem;
}

.project-link {
  color: var(--text-secondary);
  transition: color 0.3s ease;
}

.project-link:hover {
  color: var(--accent);
}

.project-content {
  flex: 1;
}

.project-title {
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 0.25rem;
  color: var(--text-primary);
}

.project-subtitle {
  font-size: 0.95rem;
  color: var(--accent);
  margin-bottom: 1rem;
  font-weight: 500;
}

.project-description {
  font-size: 0.95rem;
  color: var(--text-secondary);
  line-height: 1.7;
  margin-bottom: 1rem;
}

.project-features {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.project-features li {
  font-size: 0.85rem;
  color: var(--text-secondary);
  padding-left: 1.25rem;
  position: relative;
}

.project-features li::before {
  content: '▹';
  position: absolute;
  left: 0;
  color: var(--accent);
}

.project-footer {
  margin-top: auto;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.75rem;
  color: var(--text-secondary);
  background: var(--bg-secondary);
  padding: 0.375rem 0.75rem;
  border-radius: 4px;
}

@media (max-width: 768px) {
  .projects {
    padding: 5rem 1.5rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }

  .section-line {
    display: none;
  }
}
</style>
