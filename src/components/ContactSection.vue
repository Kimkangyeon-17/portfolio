<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const contacts = [
  {
    name: 'GitHub',
    icon: 'github',
    url: 'https://github.com/Kimkangyeon-17',
    description: '프로젝트 소스 코드'
  },
  {
    name: '개인 블로그',
    icon: 'blog',
    url: 'https://derek0517.tistory.com/',
    description: '학습 기록 및 기술 포스팅'
  },
  {
    name: '팀 블로그',
    icon: 'team',
    url: 'https://team-bob-blog.github.io/bob_blog.github.io/',
    description: '팀 스터디 기록'
  },
  {
    name: 'Email',
    icon: 'email',
    url: 'mailto:dio0517@naver.com',
    description: 'dio0517@naver.com'
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
    { threshold: 0.2 }
  )

  const section = document.querySelector('#contact')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="contact" class="contact">
    <div class="container" :class="{ visible: isVisible }">
      <div class="section-header">
        <span class="section-number">04</span>
        <h2 class="section-title">Contact</h2>
        <div class="section-line"></div>
      </div>

      <div class="contact-content">
        <div class="contact-intro">
          <h3>함께 성장할 기회를 기다립니다</h3>
          <p>
            새로운 도전과 협업에 항상 열려 있습니다.<br>
            프로젝트 제안, 스터디, 또는 궁금한 점이 있으시다면<br>
            편하게 연락 주세요!
          </p>
        </div>

        <div class="contact-grid">
          <a 
            v-for="contact in contacts" 
            :key="contact.name"
            :href="contact.url"
            target="_blank"
            rel="noopener"
            class="contact-card"
          >
            <div class="contact-icon">
              <!-- GitHub -->
              <svg v-if="contact.icon === 'github'" width="28" height="28" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
              </svg>
              <!-- Blog -->
              <svg v-if="contact.icon === 'blog'" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/>
                <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/>
              </svg>
              <!-- Team -->
              <svg v-if="contact.icon === 'team'" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
                <circle cx="9" cy="7" r="4"/>
                <path d="M23 21v-2a4 4 0 0 0-3-3.87"/>
                <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
              </svg>
              <!-- Email -->
              <svg v-if="contact.icon === 'email'" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                <polyline points="22,6 12,13 2,6"/>
              </svg>
            </div>
            <div class="contact-info">
              <span class="contact-name">{{ contact.name }}</span>
              <span class="contact-description">{{ contact.description }}</span>
            </div>
            <div class="contact-arrow">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M7 17L17 7M17 7H7M17 7V17"/>
              </svg>
            </div>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: 8rem 2rem;
  background: var(--bg-primary);
}

.container {
  max-width: 900px;
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

.contact-content {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.contact-intro {
  text-align: center;
}

.contact-intro h3 {
  font-size: 1.75rem;
  margin-bottom: 1rem;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.contact-intro p {
  color: var(--text-secondary);
  font-size: 1.1rem;
  line-height: 1.8;
}

.contact-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1rem;
}

.contact-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: 12px;
  padding: 1.25rem 1.5rem;
  text-decoration: none;
  transition: all 0.3s ease;
}

.contact-card:hover {
  border-color: var(--accent-primary);
  transform: translateY(-2px);
  background: var(--bg-secondary);
}

.contact-icon {
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(99, 102, 241, 0.1);
  border-radius: 10px;
  color: var(--accent-primary);
  flex-shrink: 0;
}

.contact-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.contact-name {
  font-size: 1rem;
  font-weight: 600;
  color: var(--text-primary);
}

.contact-description {
  font-size: 0.85rem;
  color: var(--text-secondary);
}

.contact-arrow {
  color: var(--text-secondary);
  opacity: 0;
  transform: translateX(-8px);
  transition: all 0.3s ease;
}

.contact-card:hover .contact-arrow {
  opacity: 1;
  transform: translateX(0);
  color: var(--accent-primary);
}

@media (max-width: 768px) {
  .contact {
    padding: 5rem 1.5rem;
  }

  .contact-grid {
    grid-template-columns: 1fr;
  }

  .section-line {
    display: none;
  }
}
</style>
