<script setup>
import { ref, onMounted } from 'vue'

const isVisible = ref(false)

const languages = [
  { 
    name: 'Python', 
    level: 60, 
    color: '#3776AB',
    icon: '<svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path fill="currentColor" d="M14.25.18l.9.2.73.26.59.3.45.32.34.34.25.34.16.33.1.3.04.26.02.2-.01.13V8.5l-.05.63-.13.55-.21.46-.26.38-.3.31-.33.25-.35.19-.35.14-.33.1-.3.07-.26.04-.21.02H8.77l-.69.05-.59.14-.5.22-.41.27-.33.32-.27.35-.2.36-.15.37-.1.35-.07.32-.04.27-.02.21v3.06H3.17l-.21-.03-.28-.07-.32-.12-.35-.18-.36-.26-.36-.36-.35-.46-.32-.59-.28-.73-.21-.88-.14-1.05-.05-1.23.06-1.22.16-1.04.24-.87.32-.71.36-.57.4-.44.42-.33.42-.24.4-.16.36-.1.32-.05.24-.01h.16l.06.01h8.16v-.83H6.18l-.01-2.75-.02-.37.05-.34.11-.31.17-.28.25-.26.31-.23.38-.2.44-.18.51-.15.58-.12.64-.1.71-.06.77-.04.84-.02 1.27.05zm-6.3 1.98l-.23.33-.08.41.08.41.23.34.33.22.41.09.41-.09.33-.22.23-.34.08-.41-.08-.41-.23-.33-.33-.22-.41-.09-.41.09zm13.09 3.95l.28.06.32.12.35.18.36.27.36.35.35.47.32.59.28.73.21.88.14 1.04.05 1.23-.06 1.23-.16 1.04-.24.86-.32.71-.36.57-.4.45-.42.33-.42.24-.4.16-.36.09-.32.05-.24.02-.16-.01h-8.22v.82h5.84l.01 2.76.02.36-.05.34-.11.31-.17.29-.25.25-.31.24-.38.2-.44.17-.51.15-.58.13-.64.09-.71.07-.77.04-.84.01-1.27-.04-1.07-.14-.9-.2-.73-.25-.59-.3-.45-.33-.34-.34-.25-.34-.16-.33-.1-.3-.04-.25-.02-.2.01-.13v-5.34l.05-.64.13-.54.21-.46.26-.38.3-.32.33-.24.35-.2.35-.14.33-.1.3-.06.26-.04.21-.02.13-.01h5.84l.69-.05.59-.14.5-.21.41-.28.33-.32.27-.35.2-.36.15-.36.1-.35.07-.32.04-.28.02-.21V6.07h2.09l.14.01zm-6.47 14.25l-.23.33-.08.41.08.41.23.33.33.23.41.08.41-.08.33-.23.23-.33.08-.41-.08-.41-.23-.33-.33-.23-.41-.08-.41.08z"/></svg>'
  },
  { 
    name: 'Go', 
    level: 30, 
    color: '#00ADD8',
    icon: '<svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path fill="currentColor" d="M1.811 10.231c-.047 0-.058-.023-.035-.059l.246-.315c.023-.035.081-.058.128-.058h4.172c.046 0 .058.035.035.07l-.199.303c-.023.036-.082.07-.117.07zM.047 11.306c-.047 0-.059-.023-.035-.058l.245-.316c.023-.035.082-.058.129-.058h5.328c.047 0 .07.035.058.07l-.093.28c-.012.047-.058.07-.105.07zm2.828 1.075c-.047 0-.059-.035-.035-.07l.163-.292c.023-.035.07-.07.117-.07h2.337c.047 0 .07.035.07.082l-.023.28c0 .047-.047.082-.082.082zm12.129-2.36c-.736.187-1.239.327-1.963.514-.176.046-.187.058-.34-.117-.174-.199-.303-.327-.548-.444-.737-.362-1.45-.257-2.115.175-.795.514-1.204 1.274-1.192 2.22.011.935.654 1.706 1.577 1.835.795.105 1.46-.175 1.987-.77.105-.13.198-.27.315-.434H10.47c-.245 0-.304-.152-.222-.35.152-.362.432-.97.596-1.274a.315.315 0 01.292-.187h4.253c-.023.316-.023.631-.07.947a4.983 4.983 0 01-.958 2.29c-.841 1.11-1.94 1.8-3.33 1.986-1.145.152-2.209-.07-3.143-.77-.865-.655-1.356-1.52-1.484-2.595-.152-1.274.222-2.419.993-3.424.83-1.086 1.928-1.776 3.272-2.02 1.098-.2 2.15-.07 3.096.571.62.41 1.063.97 1.356 1.648.07.105.023.164-.117.2m3.868 6.461c-1.064-.024-2.034-.328-2.852-1.029a3.665 3.665 0 01-1.262-2.255c-.21-1.32.152-2.489.947-3.529.853-1.122 1.881-1.706 3.272-1.95 1.192-.21 2.314-.095 3.33.595.923.63 1.496 1.484 1.648 2.605.198 1.578-.257 2.863-1.344 3.962-.771.783-1.718 1.273-2.805 1.495-.315.06-.63.07-.934.106zm2.78-4.72c-.011-.153-.011-.27-.034-.387-.21-1.157-1.274-1.81-2.384-1.554-1.087.245-1.788.935-2.045 2.033-.21.912.234 1.835 1.075 2.21.643.28 1.285.244 1.905-.07.923-.48 1.425-1.228 1.484-2.233z"/></svg>'
  },
  { 
    name: 'Java', 
    level: 20, 
    color: '#ED8B00',
    icon: '<svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path fill="currentColor" d="M8.851 18.56s-.917.534.653.714c1.902.218 2.874.187 4.969-.211 0 0 .552.346 1.321.646-4.699 2.013-10.633-.118-6.943-1.149M8.276 15.933s-1.028.761.542.924c2.032.209 3.636.227 6.413-.308 0 0 .384.389.987.602-5.679 1.661-12.007.13-7.942-1.218M13.116 11.475c1.158 1.333-.304 2.533-.304 2.533s2.939-1.518 1.589-3.418c-1.261-1.772-2.228-2.652 3.007-5.688 0-.001-8.216 2.051-4.292 6.573M19.33 20.504s.679.559-.747.991c-2.712.822-11.288 1.069-13.669.033-.856-.373.75-.89 1.254-.998.527-.114.828-.093.828-.093-.953-.671-6.156 1.317-2.643 1.887 9.58 1.553 17.462-.7 14.977-1.82M9.292 13.21s-4.362 1.036-1.544 1.412c1.189.159 3.561.123 5.77-.062 1.806-.152 3.618-.477 3.618-.477s-.637.272-1.098.587c-4.429 1.165-12.986.623-10.522-.568 2.082-1.006 3.776-.892 3.776-.892M17.116 17.584c4.503-2.34 2.421-4.589.968-4.285-.355.074-.515.138-.515.138s.132-.207.385-.297c2.875-1.011 5.086 2.981-.928 4.562 0-.001.07-.062.09-.118M14.401 0s2.494 2.494-2.365 6.33c-3.896 3.077-.888 4.832-.001 6.836-2.274-2.053-3.943-3.858-2.824-5.539 1.644-2.469 6.197-3.665 5.19-7.627M9.734 23.924c4.322.277 10.959-.153 11.116-2.198 0 0-.302.775-3.572 1.391-3.688.694-8.239.613-10.937.168 0-.001.553.457 3.393.639"/></svg>'
  }
]

const backend = [
  { name: 'Django', icon: '🌿' },
  { name: 'Django REST Framework', icon: '🔗' }
]

const tools = [
  { name: 'Git', icon: '📦' },
  { name: 'GitHub', icon: '🐙' },
  { name: 'VS Code', icon: '💻' },
  { name: 'PostgreSQL', icon: '🐘' },
  { name: 'SQLite', icon: '💾' }
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

  const section = document.querySelector('#skills')
  if (section) observer.observe(section)
})
</script>

<template>
  <section id="skills" class="skills">
    <div class="container" :class="{ visible: isVisible }">
      <div class="section-header">
        <span class="section-number">02</span>
        <h2 class="section-title">Skills</h2>
        <div class="section-line"></div>
      </div>

      <div class="skills-grid">
        <!-- Languages -->
        <div class="skill-category">
          <h3 class="category-title">
            <span class="category-icon">💻</span>
            Languages
          </h3>
          <div class="language-bars">
            <div v-for="lang in languages" :key="lang.name" class="language-item">
              <div class="language-info">
                <div class="language-name-wrapper">
                  <span class="language-icon" :style="{ color: lang.color }" v-html="lang.icon"></span>
                  <span class="language-name">{{ lang.name }}</span>
                </div>
                <span class="language-percent">{{ lang.level }}%</span>
              </div>
              <div class="progress-bar">
                <div 
                  class="progress-fill" 
                  :style="{ 
                    width: isVisible ? lang.level + '%' : '0%',
                    background: lang.color 
                  }"
                ></div>
              </div>
            </div>
          </div>
        </div>

        <!-- Backend -->
        <div class="skill-category">
          <h3 class="category-title">
            <span class="category-icon">⚙️</span>
            Backend
          </h3>
          <div class="skill-tags">
            <div v-for="skill in backend" :key="skill.name" class="skill-tag backend-tag">
              <span class="tag-icon">{{ skill.icon }}</span>
              <span>{{ skill.name }}</span>
            </div>
          </div>
        </div>

        <!-- Tools -->
        <div class="skill-category">
          <h3 class="category-title">
            <span class="category-icon">🛠️</span>
            Tools & Environment
          </h3>
          <div class="skill-tags">
            <div v-for="tool in tools" :key="tool.name" class="skill-tag tool-tag">
              <span class="tag-icon">{{ tool.icon }}</span>
              <span>{{ tool.name }}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="skills-note">
        <p>💡 현재 Django와 DRF를 중심으로 백엔드 개발 역량을 키우고 있으며, 지속적으로 새로운 기술을 학습하고 있습니다.</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills {
  padding: 8rem 2rem;
  background: var(--bg-primary);
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

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
}

.skill-category {
  background: var(--bg-card);
  padding: 2rem;
  border-radius: 16px;
  border: 1px solid var(--border-color);
}

.category-title {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 1.1rem;
  margin-bottom: 1.5rem;
  color: var(--text-primary);
}

.category-icon {
  font-size: 1.5rem;
}

/* Language Progress Bars */
.language-bars {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.language-item {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.language-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.language-name-wrapper {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.language-icon {
  width: 20px;
  height: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.language-icon :deep(svg) {
  width: 100%;
  height: 100%;
}

.language-name {
  font-size: 0.95rem;
  color: var(--text-primary);
  font-weight: 500;
}

.language-percent {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.8rem;
  color: var(--text-secondary);
}

.progress-bar {
  height: 8px;
  background: var(--bg-secondary);
  border-radius: 4px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  border-radius: 4px;
  transition: width 1s ease-out;
  transition-delay: 0.3s;
}

/* Skill Tags */
.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.skill-tag {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.625rem 1rem;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.3s ease;
}

.backend-tag {
  background: rgba(34, 197, 94, 0.1);
  color: #22c55e;
  border: 1px solid rgba(34, 197, 94, 0.2);
}

.backend-tag:hover {
  background: rgba(34, 197, 94, 0.2);
  transform: translateY(-2px);
}

.tool-tag {
  background: rgba(99, 102, 241, 0.1);
  color: var(--accent-primary);
  border: 1px solid rgba(99, 102, 241, 0.2);
}

.tool-tag:hover {
  background: rgba(99, 102, 241, 0.2);
  transform: translateY(-2px);
}

.tag-icon {
  font-size: 1rem;
}

.skills-note {
  margin-top: 2rem;
  padding: 1.25rem 1.5rem;
  background: rgba(99, 102, 241, 0.05);
  border-left: 3px solid var(--accent-primary);
  border-radius: 0 8px 8px 0;
}

.skills-note p {
  color: var(--text-secondary);
  font-size: 0.95rem;
}

@media (max-width: 768px) {
  .skills {
    padding: 5rem 1.5rem;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }

  .section-line {
    display: none;
  }
}
</style>
