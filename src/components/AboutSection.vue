<script setup>
import { ref, onMounted } from 'vue'

// 1. 이미지를 import 구문으로 불러옵니다.
// (components 폴더에서 상위 폴더인 src로 나갔다가 images로 들어가는 상대 경로입니다)
import ssafyLogo from '../images/ssafy_image.png'
import modulabsLogo from '../images/image_2.png'
// 파일 탐색기에 image.png가 있는 것으로 보아 CJ 로고로 추정됩니다.
// 만약 파일명이 다르다면 import cjLogo from '../images/image_2.png' 등으로 수정하세요.
import cjLogo from '../images/ci_Bioetc._01.jpg'

const isVisible = ref(false)

// 교육 및 활동 데이터
const educationHistory = [
  {
    id: 1,
    org: 'SSAFY',
    role: '14기 교육생',
    period: '2025.07 ~',
    desc: '삼성 청년 SW 아카데미',
    detail: '알고리즘 및 웹 개발 심화 과정',
    logoUrl: ssafyLogo, // 2. 여기서 import한 변수를 사용합니다 (따옴표 없음)
  },
  {
    id: 2,
    org: '모두의 연구소',
    role: '오름 캠프 Backend 3기',
    period: '2024.11.27 ~ 2025.03.24',
    desc: 'Python, Django 기반 백엔드 개발 과정',
    detail: '개인 프로젝트 블로그 및 ICT 교육 플랫폼 개발 경험',
    logoUrl: modulabsLogo, // 변수 사용
  },
  {
    id: 3,
    org: 'CJ OliveNetworks',
    role: 'Remote Internship',
    period: '2024.05.13 ~ 2024.08.08',
    desc: 'Excel을 활용한 데이터 분석 실무',
    detail: 'DS 인증 평가 통과 및 Data Science 인증서 취득',
    logoUrl: cjLogo, // 변수 사용
  },
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
    { threshold: 0.2 },
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
            생명공학을 전공하다가 개발의 매력에 빠져 새로운 도전을 시작했습니다. 현재
            <span class="accent">SSAFY(삼성 청년 SW 아카데미)</span>에서 Python과 Django를 중심으로
            백엔드 개발을 공부하고 있습니다.
          </p>
          <p>
            꾸준함을 가장 큰 무기로 삼아, 매일 조금씩 성장하는 개발자가 되기 위해 노력하고 있습니다.
            새로운 기술을 배우고 적용하는 것을 즐기며, 문제 해결 과정에서 얻는 성취감을 원동력으로
            삼고 있습니다.
          </p>
        </div>

        <div class="education-section">
          <h3 class="subsection-title">Education & Experience</h3>
          <div class="education-list">
            <div v-for="item in educationHistory" :key="item.id" class="edu-card">
              <div class="edu-logo-wrapper">
                <img :src="item.logoUrl" :alt="item.org" class="edu-logo" />
              </div>
              <div class="edu-info">
                <div class="edu-header">
                  <h4 class="edu-org">{{ item.org }}</h4>
                  <span class="edu-period">{{ item.period }}</span>
                </div>
                <div class="edu-role">{{ item.role }}</div>
                <p class="edu-desc">{{ item.desc }}</p>
                <p class="edu-detail" v-if="item.detail">- {{ item.detail }}</p>
              </div>
            </div>
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
  display: flex;
  flex-direction: column;
  gap: 4rem; /* 텍스트와 교육 섹션 사이 간격 */
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

/* Education Section Styling */
.subsection-title {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 2rem;
  color: var(--text-primary);
  border-left: 4px solid var(--accent-primary);
  padding-left: 1rem;
}

.education-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.edu-card {
  display: flex;
  gap: 2rem;
  background: var(--bg-card);
  padding: 1.5rem 2rem;
  border-radius: 16px;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
  align-items: center;
}

.edu-card:hover {
  border-color: var(--accent-primary);
  transform: translateX(5px);
  background: rgba(255, 255, 255, 0.03);
}

.edu-logo-wrapper {
  width: 80px;
  height: 80px;
  background: #fff; /* 로고가 잘 보이도록 흰 배경 */
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  flex-shrink: 0;
  overflow: hidden;
}

.edu-logo {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

.edu-info {
  flex: 1;
}

.edu-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.edu-org {
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--text-primary);
}

.edu-period {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.9rem;
  color: var(--text-secondary);
  background: rgba(99, 102, 241, 0.1);
  padding: 0.2rem 0.6rem;
  border-radius: 4px;
}

.edu-role {
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--accent-primary);
  margin-bottom: 0.5rem;
}

.edu-desc {
  color: var(--text-secondary);
  font-size: 0.95rem;
  margin-bottom: 0.2rem;
}

.edu-detail {
  color: var(--text-secondary);
  font-size: 0.9rem;
  opacity: 0.8;
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

  .edu-card {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
    padding: 1.5rem;
  }

  .edu-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.25rem;
  }

  .edu-period {
    font-size: 0.8rem;
  }

  .edu-logo-wrapper {
    width: 60px;
    height: 60px;
  }
}
</style>
