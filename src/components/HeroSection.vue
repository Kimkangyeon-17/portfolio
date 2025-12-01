<script setup>
import { ref, onMounted } from 'vue'
import profileImage from '@/assets/profile.png'

const isVisible = ref(false)

const personalInfo = {
  name: '김강연',
  nameEn: 'Kim Kangyeon',
  birth: '1999.05.10',
  major: '생명공학부 바이오소재전공',
  email: 'dio0517@naver.com',
  tagline: '꾸준함으로 성장하는 백엔드 개발자',
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

    <div class="hero-container" :class="{ visible: isVisible }">
      <!-- 왼쪽: 프로필 이미지 -->
      <div class="hero-image">
        <div class="image-wrapper">
          <img :src="profileImage" alt="김강연 프로필" />
          <div class="image-glow"></div>
        </div>
      </div>

      <!-- 오른쪽: 텍스트 콘텐츠 -->
      <div class="hero-content">
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

/* 메인 컨테이너 - 2열 레이아웃 */
.hero-container {
  display: flex;
  align-items: center;
  gap: 4rem;
  max-width: 1200px;
  width: 100%;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.hero-container.visible {
  opacity: 1;
  transform: translateY(0);
}

/* 왼쪽: 프로필 이미지 */
.hero-image {
  flex: 0 0 auto;
}

.image-wrapper {
  position: relative;
  width: 420px;
  height: 540px;
}

.image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  object-position: bottom;
  position: relative;
  z-index: 2;
  filter: drop-shadow(0 20px 40px rgba(0, 0, 0, 0.3));
}

.image-glow {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 80%;
  height: 60%;
  background: var(--accent-gradient);
  filter: blur(80px);
  opacity: 0.3;
  z-index: 1;
  border-radius: 50%;
}

/* 오른쪽: 텍스트 콘텐츠 */
.hero-content {
  flex: 1;
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
  font-size: clamp(2rem, 5vw, 3.5rem);
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
  font-size: 0.35em;
  color: var(--text-secondary);
  font-weight: 400;
  font-family: 'JetBrains Mono', monospace;
  margin-top: 0.5rem;
}

.role {
  color: var(--text-primary);
  font-weight: 300;
}

.hero-tagline {
  font-size: 1.125rem;
  color: var(--text-secondary);
  margin-bottom: 2rem;
  max-width: 450px;
}

.info-cards {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-bottom: 2rem;
}

.info-card {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  background: var(--bg-card);
  padding: 0.75rem 1rem;
  border-radius: 10px;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.info-card:hover {
  border-color: var(--accent-primary);
  transform: translateY(-2px);
}

.info-icon {
  font-size: 1.25rem;
}

.info-content {
  display: flex;
  flex-direction: column;
}

.info-label {
  font-size: 0.7rem;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.info-value {
  font-size: 0.85rem;
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
  padding: 0.75rem 1.25rem;
  border-radius: 8px;
  font-size: 0.875rem;
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

/* 반응형 - 태블릿 & 모바일 */
@media (max-width: 968px) {
  .hero-container {
    flex-direction: column;
    text-align: center;
    gap: 2rem;
  }

  .hero-image {
    order: -1;
  }

  .image-wrapper {
    width: 320px;
    height: 410px;
  }

  .hero-content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .info-cards {
    justify-content: center;
  }

  .hero-cta {
    justify-content: center;
  }

  .hero-tagline {
    text-align: center;
  }
}

@media (max-width: 600px) {
  .hero {
    padding: 5rem 1.5rem 3rem;
  }

  .image-wrapper {
    width: 260px;
    height: 330px;
  }

  .info-cards {
    flex-direction: column;
    align-items: stretch;
  }

  .hero-cta {
    flex-direction: column;
    width: 100%;
  }

  .btn {
    justify-content: center;
  }
}
</style>
