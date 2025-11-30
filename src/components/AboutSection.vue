<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

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

  const section = document.querySelector('#about')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="about" class="about">
    <div class="container" :class="{ visible: isVisible }">
      <div class="section-header">
        <span class="section-number">01</span>
        <h2 class="section-title">About Me</h2>
        <div class="section-line"></div>
      </div>

      <div class="about-content">
        <div class="about-text">
          <p class="highlight">
            안녕하세요! 저는 <span class="accent">백엔드 개발자</span>를 꿈꾸는 김강연입니다.
          </p>
          <p>
            생명공학을 전공하다가 개발의 매력에 빠져 새로운 도전을 시작했습니다.
            현재 <span class="accent">SSAFY(삼성 청년 SW 아카데미)</span>에서 
            Python과 Django를 중심으로 백엔드 개발을 공부하고 있습니다.
          </p>
          <p>
            꾸준함을 가장 큰 무기로 삼아, 매일 조금씩 성장하는 개발자가 되기 위해 노력하고 있습니다.
            새로운 기술을 배우고 적용하는 것을 즐기며, 문제 해결 과정에서 얻는 성취감을 
            원동력으로 삼고 있습니다.
          </p>
        </div>

        <div class="about-highlights">
          <div class="highlight-card">
            <div class="highlight-icon">🎯</div>
            <h3>목표</h3>
            <p>사용자에게 가치를 전달하는 안정적인 서비스를 만드는 백엔드 개발자</p>
          </div>
          <div class="highlight-card">
            <div class="highlight-icon">📚</div>
            <h3>학습</h3>
            <p>SSAFY에서 Django, DRF, 알고리즘 등 실무 중심의 개발 역량 강화 중</p>
          </div>
          <div class="highlight-card">
            <div class="highlight-icon">🚀</div>
            <h3>성장</h3>
            <p>블로그와 스터디를 통해 배운 것을 기록하고 공유하며 함께 성장</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
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

.about-content {
  display: grid;
  gap: 3rem;
}

.about-text {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.about-text p {
  font-size: 1.1rem;
  color: var(--text-secondary);
  line-height: 1.8;
}

.about-text .highlight {
  font-size: 1.3rem;
  color: var(--text-primary);
}

.accent {
  color: var(--accent-primary);
  font-weight: 500;
}

.about-highlights {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

.highlight-card {
  background: var(--bg-card);
  padding: 2rem;
  border-radius: 16px;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.highlight-card:hover {
  border-color: var(--accent-primary);
  transform: translateY(-4px);
}

.highlight-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.highlight-card h3 {
  font-size: 1.1rem;
  margin-bottom: 0.75rem;
  color: var(--text-primary);
}

.highlight-card p {
  font-size: 0.95rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

@media (max-width: 768px) {
  .about {
    padding: 5rem 1.5rem;
  }

  .section-header {
    flex-wrap: wrap;
  }

  .section-line {
    display: none;
  }
}
</style>
