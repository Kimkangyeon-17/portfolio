<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const personalInfo = {
  name: '김강연',
  nameEn: 'Kim Kangyeon',
  birth: '1999.05.10',
  major: '생명공학부 바이오소재전공',
  email: 'dio0517@naver.com',
  tagline: '꾸준함으로 성장하는 백엔드 개발자',
  certificates: 'SQLD(2024.04.05), ADsP(2025.11.28)',
}

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 300)
})
</script>

<template>
  <section class="hero">
    <div class="hero-bg">
      <div class="gradient-orb orb-1"></div>
      <div class="gradient-orb orb-2"></div>
      <div class="grid-pattern"></div>
    </div>

    <div class="hero-content" :class="{ visible: isVisible }">
      <div class="intro-badge">
        <span class="badge-dot"></span>
        <span>도전을 두려워하지 않는 개발자</span>
      </div>

      <h1 class="hero-title">
        <span class="greeting">안녕하세요,</span>
        <span class="name">{{ personalInfo.name }}</span>
        <span class="role">입니다.</span>
        <span class="name-en">{{ personalInfo.nameEn }}</span>
      </h1>

      <p class="hero-tagline">{{ personalInfo.tagline }}</p>

      <div class="info-cards">
        <div class="info-card">
          <span class="info-icon">🎂</span>
          <div class="info-content">
            <span class="info-label">Birth</span>
            <span class="info-value">{{ personalInfo.birth }}</span>
          </div>
        </div>
        <div class="info-card">
          <span class="info-icon">🎓</span>
          <div class="info-content">
            <span class="info-label">Major</span>
            <span class="info-value">{{ personalInfo.major }}</span>
          </div>
        </div>
        <div class="info-card">
          <span class="info-icon">📧</span>
          <div class="info-content">
            <span class="info-label">Email</span>
            <span class="info-value">{{ personalInfo.email }}</span>
          </div>
        </div>
        <div class="info-card">
          <span class="info-icon">🏆</span>
          <div class="info-content">
            <span class="info-label">Certificates</span>
            <span class="info-value">{{ personalInfo.certificates }}</span>
          </div>
        </div>
      </div>

      <div class="hero-cta">
        <a href="#projects" class="btn btn-primary">
          프로젝트 보기
          <svg
            width="20"
            height="20"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <path d="M7 17L17 7M17 7H7M17 7V17" />
          </svg>
        </a>
        <a href="#contact" class="btn btn-secondary">연락하기</a>
      </div>
    </div>

    <div class="scroll-indicator">
      <span>Scroll</span>
      <div class="scroll-line"></div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  padding: 6rem 2rem 4rem;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.gradient-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(100px);
  opacity: 0.4;
}

.orb-1 {
  width: 600px;
  height: 600px;
  background: var(--accent-primary);
  top: -200px;
  right: -200px;
  animation: float 8s ease-in-out infinite;
}

.orb-2 {
  width: 400px;
  height: 400px;
  background: var(--accent-secondary);
  bottom: -100px;
  left: -100px;
  animation: float 6s ease-in-out infinite reverse;
}

@keyframes float {
  0%,
  100% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(30px, -30px);
  }
}

.grid-pattern {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(99, 102, 241, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(99, 102, 241, 0.03) 1px, transparent 1px);
  background-size: 60px 60px;
}

.hero-content {
  max-width: 900px;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.hero-content.visible {
  opacity: 1;
  transform: translateY(0);
}

.intro-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(99, 102, 241, 0.1);
  border: 1px solid rgba(99, 102, 241, 0.2);
  padding: 0.5rem 1rem;
  border-radius: 50px;
  font-size: 0.875rem;
  color: var(--accent-primary);
  margin-bottom: 1.5rem;
}

.badge-dot {
  width: 8px;
  height: 8px;
  background: var(--accent-primary);
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

.hero-title {
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 1rem;
}

.greeting {
  display: block;
  color: var(--text-secondary);
  font-size: 0.5em;
  font-weight: 400;
  margin-bottom: 0.5rem;
}

.name {
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.name-en {
  display: block;
  font-size: 0.4em;
  color: var(--text-secondary);
  font-weight: 400;
  font-family: 'JetBrains Mono', monospace;
  margin-top: 0.25rem;
}

.role {
  color: var(--text-primary);
  font-size: 0.5em;
  font-weight: 400;
  margin-bottom: 0.5rem;
}

.hero-tagline {
  font-size: 1.25rem;
  color: var(--text-secondary);
  margin-bottom: 2.5rem;
  max-width: 500px;
}

.info-cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 2.5rem;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  background: var(--bg-card);
  padding: 1rem 1.25rem;
  border-radius: 12px;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
  /* 카드가 많아져서 유연하게 너비 조절 */
  flex: 1 1 200px;
}

.info-card:hover {
  border-color: var(--accent-primary);
  transform: translateY(-2px);
}

.info-icon {
  font-size: 1.5rem;
}

.info-content {
  display: flex;
  flex-direction: column;
}

.info-label {
  font-size: 0.75rem;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.info-value {
  font-size: 0.9rem;
  color: var(--text-primary);
  font-weight: 500;
}

.hero-cta {
  display: flex;
  gap: 1rem;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.875rem 1.5rem;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.3s ease;
}

.btn-primary {
  background: var(--accent-gradient);
  color: white;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(99, 102, 241, 0.3);
}

.btn-secondary {
  background: transparent;
  color: var(--text-primary);
  border: 1px solid var(--border-color);
}

.btn-secondary:hover {
  border-color: var(--accent-primary);
  color: var(--accent-primary);
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: var(--text-secondary);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.scroll-line {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, var(--accent-primary), transparent);
  animation: scrollLine 2s ease-in-out infinite;
}

@keyframes scrollLine {
  0%,
  100% {
    transform: scaleY(1);
    opacity: 1;
  }
  50% {
    transform: scaleY(0.5);
    opacity: 0.5;
  }
}

@media (max-width: 768px) {
  .hero {
    padding: 5rem 1.5rem 3rem;
  }

  .info-cards {
    flex-direction: column;
    align-items: stretch;
  }

  .info-card {
    flex: initial;
  }

  .hero-cta {
    flex-direction: column;
  }

  .btn {
    justify-content: center;
  }
}
</style>
