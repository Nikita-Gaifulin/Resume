<script setup>
import { ref } from 'vue'
import { MapPin, Mail, GithubCircle, Telegram , SunLight, HalfMoon} from '@iconoir/vue'

const photoUrl = './logo.png'

const personal = ref({
  name: 'Никита Гайфулин',
  title: 'Frontend-разработчик',
  location: 'Санкт-Петербург, Россия',
  email: 'nik141196@gmail.com',
  github: 'github.com/Nikita-Gaifulin',
  telegram: '@N8K8TA',
  about: 'Привет! Я Frontend разработчик с 6+ годами опыта в нефтегазовой отрасли в компании международного уровня (Emerson). Решаю инженерные задачи повышенной сложности 👷🏻‍🛠️. Нравится создавать не только качественный, но и эстетически красивый продукт✨. Имею опыт взаимодействия с международными командами (English — Intermediate)🇬🇧. Вне работы люблю теннис, тренажерный зал, читать классику и много гулять.'
})

const skills = ref([
  { name: 'Vue 3', level: 'продвинутый' },
  { name: 'TypeScript', level: 'продвинутый' },
  { name: 'Tailwind CSS', level: 'продвинутый' },
  { name: 'HTML', level: 'продвинутый' },
  { name: 'Docker', level: 'продвинутый' },
  { name: 'Cypress', level: 'продвинутый' },
  { name: 'Jest', level: 'продвинутый' },
  { name: 'Git / GitHub', level: 'продвинутый' }
])

const experience = ref([
  {
    company: 'Emerson',
    period: '2020 — 2022',
    role: 'Frontend-разработчик С# + ручной тестер',
    achievements: [
      'разработка desktop приложения на WPF для мониторинга физических величин',
      'участвовал в покрытии страниц автотестами на Selenium + Appium',
      'участвовал в покрытии кода тестами на NUnit',
      'менторство членов команды + выполнял роль скрам мастера'
    ]
  },
  {
    company: 'Метраникс (Метран)',
    period: '2022 — 2026',
    role: 'Frontend-разработчик',
    achievements: [
      'разработка визуализации данных с использованием Chart.js.',
      'доработка интерпретатора C-подобного языка на TypeScript.',
      'автоматизация тестирования: UI-тесты (Cypress), unit-тесты (Jest).',
      'работа с англоязыной документацией зарубежных коллег.',
      'менторство новых членов команды, проведение code review с контролем соблюдения архитектурных стандартов.',
      'активное участие в code review с фокусом на качество кода и поддерживаемость.'
    ]
  }
])

// ========== ТЕМНАЯ ТЕМА ==========
const isDark = ref(true) // поставил темную по умолчанию (круто смотрится)

function toggleTheme() {
  isDark.value = !isDark.value
}
</script>

<template>
  <div :class="['app', { dark: isDark }]">
    <div class="container">
      <!-- Кнопка переключения темы -->
      <button class="theme-toggle" @click="toggleTheme">
        <SunLight v-if="!isDark" color="#000" :size="18"/>
        <HalfMoon v-else color="#FFF" :size="18"/>
      </button>

      <!-- Основная сетка -->
      <div class="grid">
        <!-- ЛЕВАЯ КОЛОНКА (фото, контакты, навыки) -->
        <aside class="sidebar">
          <div class="photo-wrapper">
            <img :src="photoUrl" alt="Здесь должно было быть фото:(" class="photo" @error="(e) => e.target.src = 'https://via.placeholder.com/200?text=Фото'" />
          </div>

          <h1 class="name">{{ personal.name }}</h1>
          <p class="title">{{ personal.title }}</p>

          <div class="contacts">
            <p><MapPin class="contact-icon" :size="18" /> {{ personal.location }}</p>
            <p><Mail class="contact-icon" :size="18" /> {{ personal.email }}</p>
            <p>
              <GithubCircle class="contact-icon" :size="18" />
              <a :href="`https://${personal.github}`" target="_blank" rel="noopener noreferrer" class="contact-link">
                {{ personal.github }}
              </a>
            </p>
            <p>
      <Telegram class="contact-icon" :size="18" />
      <a :href="`https://t.me/${personal.telegram.replace('@', '')}`" target="_blank" rel="noopener noreferrer" class="contact-link">
        {{ personal.telegram }}
      </a>
    </p>
          </div>

          <div class="skills">
            <h3>Навыки</h3>
            <div class="skill-tags">
              <span v-for="skill in skills" :key="skill.name" class="skill-tag">
                {{ skill.name }}
                <small>({{ skill.level }})</small>
              </span>
            </div>
          </div>

          <div class="OS">
            <h3>OS</h3>
            <p class="OS-names">Linux, Windows</p>
          </div>
        </aside>

        <!-- ПРАВАЯ КОЛОНКА (опыт, проекты, о себе) -->
        <main class="content">
          <section>
            <h2>О себе</h2>
            <p class="about-text">{{ personal.about }}</p>
          </section>

          <section>
            <h2>Опыт работы</h2>
            <div v-for="job in experience" :key="job.company" class="job-item">
              <div class="job-header">
                <h3>{{ job.company }}</h3>
                <span class="period">{{ job.period }}</span>
              </div>
              <p class="role">{{ job.role }}</p>
              <ul>
                <li v-for="achievement in job.achievements" :key="achievement">
                  {{ achievement }}
                </li>
              </ul>
            </div>
          </section>

          <footer class="footer">
            <p>Открыт к сотрудничеству ✨</p>
          </footer>
        </main>
      </div>
    </div>
  </div>
</template>

<style>
/* Глобальные сбросы */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
  background: #f4f4f4;
  transition: background 0.3s;
}

/* Темная тема через CSS переменные */
.app {
  --bg-page: #f4f4f4;
  --card-bg: #ffffff;
  --text-primary: #1a1a1a;
  --text-secondary: #4a4a4a;
  --border: #e0e0e0;
  --accent: #3b82f6;
  --tag-bg: #eef2ff;
}

.app.dark {
  --bg-page: #0f172a;
  --card-bg: #1e293b;
  --text-primary: #f1f5f9;
  --text-secondary: #94a3b8;
  --border: #334155;
  --accent: #60a5fa;
  --tag-bg: #1e293b;
}

.app {
  background: var(--bg-page);
  color: var(--text-primary);
  min-height: 100vh;
  transition: all 0.3s;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem 1.5rem;
  position: relative;
}

.theme-icon {
  color: #FFF;
}

/* Кнопка темы */
.theme-toggle {
  position: fixed;
  top: 1rem;
  right: 1rem;
  background: var(--card-bg);
  border: 1px solid var(--border);
  font-size: 1.5rem;
  padding: 0.5rem 1rem;
  border-radius: 40px;
  cursor: pointer;
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.2s;
}
.theme-toggle:hover {
  transform: scale(1.05);
}

/* Сетка */
.grid {
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 2rem;
}

/* ЛЕВАЯ КОЛОНКА */
.sidebar {
  background: var(--card-bg);
  border-radius: 24px;
  padding: 1.8rem;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  border: 1px solid var(--border);
  height: fit-content;
  animation: slideInLeft 0.6s ease-out forwards;
  opacity: 0;
}

.photo-wrapper {
  display: flex;
  justify-content: center;
  margin-bottom: 1.5rem;
}

.photo {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid var(--accent);
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
  transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
  cursor: pointer;
}

.photo:hover {
  transform: scale(1.2);
  box-shadow: 0 12px 28px rgba(0,0,0,0.2);
}

.name {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
  text-align: center;
}

.title {
  color: var(--accent);
  font-weight: 500;
  text-align: center;
  margin-bottom: 1.5rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid var(--border);
}

.contacts {
  margin: 1.5rem 0;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  font-size: 0.9rem;
  color: var(--text-primary);
}

.OS {
  gap: 0.6rem;
  margin: 1.5rem 0;
}

.OS-names {
  display: flex;
  margin: 1rem 0;
  margin-left: 1rem;
  font-size: 0.9rem;
  color: var(--text-primary);
}

.contacts p {
  word-break: break-word;
}

.contact-icon {
  vertical-align: middle;
  padding-right: 0.1rem;
}

.contact-link {
  color: var(--text-primary);
  text-decoration: none;
  transition: color 0.2s ease;
}

.contact-link:hover {
  color: var(--text-secondary);
  text-decoration: underline;
}

.skills h3 {
  margin-bottom: 1rem;
  font-size: 1.2rem;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.skill-tag {
  background: var(--tag-bg);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 500;
  border: 1px solid var(--border);
}

.skill-tag:hover {
  animation: shake 0.2s ease-in-out 0s 2;
}

@keyframes shake {
  0% { transform: translateX(0); }
  25% { transform: translateX(-2px); }
  75% { transform: translateX(2px); }
  100% { transform: translateX(0); }
}

.skill-tag small {
  font-weight: normal;
  opacity: 0.7;
  font-size: 0.7rem;
}

/* ПРАВАЯ КОЛОНКА */
.content {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  animation: slideInRight 0.6s ease-out forwards;
  opacity: 0;
  animation-delay: 0.2s;
}

section {
  background: var(--card-bg);
  border-radius: 24px;
  padding: 1.8rem;
  border: 1px solid var(--border);
  transition: transform 0.2s;
  animation: fadeScale 0.5s ease-out forwards;
  opacity: 0;
}

section:hover {
  transform: translateY(-2px);
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 1.2rem;
  border-left: 4px solid var(--accent);
  padding-left: 0.8rem;
}

.about-text {
  line-height: 1.6;
  color: var(--text-secondary);
}

.job-item {
  margin-bottom: 1.8rem;
  padding-bottom: 1.2rem;
  border-bottom: 1px solid var(--border);
}
.job-item:last-child {
  border-bottom: none;
  margin-bottom: 0;
}

.job-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 0.3rem;
}

.job-header h3 {
  font-size: 1.2rem;
}

.period {
  font-size: 0.85rem;
  color: var(--accent);
  font-weight: 500;
}

.role {
  font-weight: 500;
  margin-bottom: 0.8rem;
  color: var(--text-secondary);
  font-size: 0.9rem;
}

ul {
  padding-left: 1.5rem;
  color: var(--text-secondary);
}

li {
  margin: 0.5rem 0;
  line-height: 1.4;
}

.project-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.project-card {
  padding: 1rem;
  background: var(--tag-bg);
  border-radius: 16px;
  transition: all 0.2s;
}
.project-card:hover {
  background: var(--border);
}

.project-card h3 {
  font-size: 1rem;
  margin-bottom: 0.3rem;
}
.project-card p {
  font-size: 0.85rem;
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}
.project-card a {
  color: var(--accent);
  text-decoration: none;
  font-size: 0.85rem;
  font-weight: 500;
}

.footer {
  text-align: center;
  padding: 1rem;
  font-size: 0.9rem;
  color: var(--text-secondary);
}

section:nth-child(1) { animation-delay: 0.3s; }
section:nth-child(2) { animation-delay: 0.4s; }
section:nth-child(3) { animation-delay: 0.5s; }
section:nth-child(4) { animation-delay: 0.6s; }

@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeScale {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* Адаптив */
@media (max-width: 768px) {
  .grid {
    grid-template-columns: 1fr;
  }

  .container {
    padding: 1rem;
  }

  .sidebar {
    text-align: center;
  }

  .contacts {
    align-items: center;
  }

  .skill-tags {
    justify-content: center;
  }

  .job-header {
    flex-direction: column;
  }
}
</style>