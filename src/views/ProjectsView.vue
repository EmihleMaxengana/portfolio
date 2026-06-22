<template>
  <main class="projects">
    <div class="projects__orb projects__orb--1" aria-hidden="true"></div>
    <div class="projects__orb projects__orb--2" aria-hidden="true"></div>

    <div class="projects__container">
      <div class="projects__header">
        <h1 class="projects__title glitch-text" data-text="Projects">Projects</h1>
        <p class="projects__subtitle">Some things I've built</p>
      </div>

      <div class="carousel-container">
        <button class="carousel-btn prev-btn" @click="prevSlide" aria-label="Previous">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M15 18l-6-6 6-6"/>
          </svg>
        </button>

        <div class="carousel-wrapper">
          <div class="carousel-track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
            <div v-for="(chunk, slideIndex) in projectChunks" :key="slideIndex" class="carousel-slide">
              <div class="slide-grid">
                <div v-for="project in chunk" :key="project.title" class="project-card" @click="openModal(project)">
                  <div class="project-card__image">
                    <img 
                      :src="project.image" 
                      :alt="project.title"
                      loading="lazy"
                    />
                  </div>
                  <div class="project-card__content">
                    <h3 class="project-card__title">{{ project.title }}</h3>
                    <p class="project-card__description">{{ project.description }}</p>
                    <div class="project-card__tags">
                      <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                    </div>
                    <div class="project-card__links">
                      <a v-if="project.demo" :href="project.demo" target="_blank" rel="noopener noreferrer" class="project-link" @click.stop>Live Demo</a>
                      <a v-if="project.code" :href="project.code" target="_blank" rel="noopener noreferrer" class="project-link" @click.stop>Source Code</a>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <button class="carousel-btn next-btn" @click="nextSlide" aria-label="Next">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M9 18l6-6-6-6"/>
          </svg>
        </button>
      </div>

      <div class="carousel-indicators">
        <button 
          v-for="(_, index) in projectChunks" 
          :key="index"
          @click="goToSlide(index)"
          class="indicator"
          :class="{ active: currentIndex === index }"
          :aria-label="`Go to slide ${index + 1}`"
        ></button>
      </div>
    </div>

    <Transition name="modal">
      <div v-if="selectedProject" class="modal-overlay" @click="closeModal">
        <div class="modal-content" @click.stop>
          <button class="modal-close" @click="closeModal" aria-label="Close modal">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="18" y1="6" x2="6" y2="18"/>
              <line x1="6" y1="6" x2="18" y2="18"/>
            </svg>
          </button>
          
          <div class="modal-image">
            <img :src="selectedProject.image" :alt="selectedProject.title" />
          </div>
          
          <div class="modal-body">
            <h2 class="modal-title">{{ selectedProject.title }}</h2>
            <p class="modal-description">{{ selectedProject.description }}</p>
            
            <div class="modal-tags">
              <span v-for="tag in selectedProject.tags" :key="tag" class="modal-tag">{{ tag }}</span>
            </div>
            
            <div class="modal-links">
              <a v-if="selectedProject.demo" :href="selectedProject.demo" target="_blank" rel="noopener noreferrer" class="modal-link modal-link--primary">Live Demo</a>
              <a v-if="selectedProject.code" :href="selectedProject.code" target="_blank" rel="noopener noreferrer" class="modal-link modal-link--secondary">Source Code</a>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </main>
</template>

<script>
import fullStackImage from '@/assets/FullStack.jpg'
import ECommerceImage from '@/assets/ECommerce.jpg'
import FrontEndImage from '@/assets/FrontEnd.jpg'
import MobileApplicationImage from '@/assets/MobileApplication.jpg'

export default {
  name: 'ProjectsView',
  data() {
    return {
      currentIndex: 0,
      selectedProject: null,
      projects: [
        {
          title: 'Portfolio Website',
          description: `This is a modern, single-page portfolio website built with Vue 3 and Vite, designed to showcase the skills and projects of Emihle Maxengana, 
          a Full-Stack Developer. The site features a dark, elegant aesthetic with hot pink accents and subtle glitch effects, creating a distinctive personal brand. 
          The layout includes five main sections: a hero section with a rotating role display and profile image, an About section with a bio and glitched title, a Skills
           section featuring an autoplay carousel of technology icons, a Projects section with a card-based carousel and interactive modal popups for full project details, 
           and a Contact section with both Gmail and mailto options for reaching out. The website is fully responsive, works across all devices, and includes smooth scrolling 
           navigation with a fixed header. `,
          tags: ['Vue.js', 'CSS', 'Javascript', 'HTML'],
          image: FrontEndImage,
          code: 'https://github.com/EmihleMaxengana/portfolio.git'
        },
        {
          title: 'E-Commerce Store',
          description: `Cape Route Tours is a tourism booking and management platform built with Vue.js (front-end), Node.js + Express (back-end), and MySQL (database). The system allows tourists to explore Cape Town's townships, book cultural tours, read blogs, and contact the company — while the admin can manage tours, bookings, and content.`,
          tags: ['Vue.js', 'Vue Router', 'Axios', 'Bootstrap', 'Animate.css', 'Font Awesome', 'Node.js', 'Express.js', 'MySQL'],
          image: ECommerceImage,
          demo: 'https://cape-route-tours.netlify.app',
          code: 'https://github.com/EmihleMaxengana/e-commerce-.git'
        },
        {
          title: 'Front-End',
          description: `My first frontend web application built with Vue.js to simplify and enhance Human Resources management. This system supports features like employee tracking, payroll generation, leave requests, attendance monitoring, and more — all powered by a modern frontend.`,
          tags: ['Vue.js', 'Vue Router', 'Axios', 'Bootstrap5'],
          image: FrontEndImage,
          demo: 'https://project-fronten.netlify.app/#/',
          code: 'https://github.com/EmihleMaxengana/frontend-project-1.git'
        },
        {
          title: 'Front-End',
          description: `Assessment sent by a company I applied for so I built a responsive legal workflow dashboard that displays task lists with real-time search, status/priority filtering, and a mobile-friendly layout. Beyond the core requirements, I added dark mode, sorting, debounced search, and local storage persistence to enhance usability and retain user preferences. The project showcased my ability to turn a product brief into a clean, functional UI while prioritizing reusable components, clean code, and thoughtful user experience within a tight timeframe.`,
          tags: ['Javascript', 'React', 'CSS'],
          image: FrontEndImage,
          demo: 'https://steady-otter-14ac64.netlify.app/',
          code: 'https://github.com/EmihleMaxengana/frontend-project-1.git'
        },
        {
          title: 'Mobile Application',
          description: `Purple Safety is a Flutter mobile application providing personal safety features such as 
          emergency alerts, contact management, location sharing, and safety tools. It supports Android and iOS and 
          includes platform-specific native code and integrations for Firebase and device services.`,
          tags: ['Dart', 'Flutter', 'HTML', 'Kotlin', 'CMake', 'c++', 'Swift', 'Firebase'],
          image: MobileApplicationImage
        }
      ]
    }
  },
  computed: {
    // Group projects into chunks of 3
    projectChunks() {
      const chunkSize = 3
      const chunks = []
      for (let i = 0; i < this.projects.length; i += chunkSize) {
        chunks.push(this.projects.slice(i, i + chunkSize))
      }
      return chunks
    }
  },
  methods: {
    nextSlide() {
      if (this.currentIndex < this.projectChunks.length - 1) {
        this.currentIndex++
      } else {
        this.currentIndex = 0
      }
    },
    prevSlide() {
      if (this.currentIndex > 0) {
        this.currentIndex--
      } else {
        this.currentIndex = this.projectChunks.length - 1
      }
    },
    goToSlide(index) {
      this.currentIndex = index
    },
    openModal(project) {
      this.selectedProject = project
      document.body.style.overflow = 'hidden'
    },
    closeModal() {
      this.selectedProject = null
      document.body.style.overflow = ''
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,700&family=Inter:wght@400;500;600&display=swap');

:root {
  --pink-hot: #e91e8c;
  --pink-blush: #f4a7c3;
  --pink-pale: #fdf0f5;
  --dark-base: #1a0a0f;
  --header-h: 72px;
}

.projects {
  background: var(--dark-base);
  min-height: 100vh;
  overflow-x: hidden;
}

.projects__orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
}

.projects__orb--1 {
  width: 500px;
  height: 500px;
  background: rgba(233, 30, 140, 0.12);
  top: -100px;
  left: -200px;
}

.projects__orb--2 {
  width: 360px;
  height: 360px;
  background: rgba(244, 167, 195, 0.07);
  bottom: 60px;
  right: -100px;
}

.projects__container {
  max-width: 1200px;
  margin: 0 auto;
  padding: calc(var(--header-h) + 1.5rem) 2rem 3rem;
  position: relative;
  z-index: 1;
}

.projects__header {
  text-align: center;
  margin-bottom: 4rem;
}

.projects__title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: var(--pink-hot);
  position: relative;
  display: inline-block;
  animation: glitch-skew 3s infinite ease-in-out;
}

.projects__subtitle {
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  color: rgba(244, 167, 195, 0.6);
  letter-spacing: 0.05em;
}

.glitch-text {
  position: relative;
}

.glitch-text::before,
.glitch-text::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--dark-base);
}

.glitch-text::before {
  color: #6366f1;
  z-index: -1;
  animation: glitch-1 2.2s infinite linear alternate-reverse;
}

.glitch-text::after {
  color: #ec489a;
  z-index: -2;
  animation: glitch-2 2.5s infinite linear alternate-reverse;
}

@keyframes glitch-1 {
  0%, 100% { clip-path: inset(0 0 0 0); transform: translate(0); }
  20% { clip-path: inset(10% 0 20% 0); transform: translate(-2px, 1px); }
  40% { clip-path: inset(30% 0 15% 0); transform: translate(2px, -1px); }
  60% { clip-path: inset(5% 0 35% 0); transform: translate(-1px, 0); }
  80% { clip-path: inset(50% 0 5% 0); transform: translate(1px, 1px); }
}

@keyframes glitch-2 {
  0%, 100% { clip-path: inset(0 0 0 0); transform: translate(0); }
  25% { clip-path: inset(15% 0 25% 0); transform: translate(2px, -1px); }
  50% { clip-path: inset(40% 0 10% 0); transform: translate(-2px, 2px); }
  75% { clip-path: inset(5% 0 50% 0); transform: translate(1px, -1px); }
}

@keyframes glitch-skew {
  0%, 100% { transform: skew(0deg); }
  5% { transform: skew(1.5deg); }
  10% { transform: skew(-1deg); }
  15% { transform: skew(0deg); }
}

.carousel-container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem 0;
}

.carousel-wrapper {
  overflow: hidden;
  width: 100%;
  max-width: 1100px;
  margin: 0 1rem;
}

.carousel-track {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-slide {
  flex: 0 0 100%;
  padding: 1rem 0;
}

.slide-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  justify-items: center;
}

/* Project Card */
.project-card {
  background: rgba(233, 30, 140, 0.05);
  border-radius: 24px;
  overflow: hidden;
  border: 1px solid rgba(233, 30, 140, 0.15);
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 340px;
  margin: 0 auto;
  cursor: pointer;
}

.project-card:hover {
  border-color: rgba(233, 30, 140, 0.4);
  transform: translateY(-6px);
  box-shadow: 0 12px 40px rgba(233, 30, 140, 0.15);
}

.project-card__image {
  width: 100%;
  height: 180px;
  overflow: hidden;
  background: rgba(233, 30, 140, 0.1);
}

.project-card__image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.project-card:hover .project-card__image img {
  transform: scale(1.05);
}

.project-card__content {
  padding: 1.2rem;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.project-card__title {
  font-family: 'Playfair Display', serif;
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--pink-pale);
  margin: 0 0 0.4rem;
}

.project-card__description {
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  line-height: 1.5;
  color: rgba(244, 167, 195, 0.7);
  margin: 0 0 1rem;
  flex: 1;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.project-card__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin-bottom: 1rem;
}

.project-card__tags span {
  font-family: 'Inter', sans-serif;
  font-size: 0.65rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  background: rgba(233, 30, 140, 0.15);
  color: var(--pink-blush);
  padding: 0.2rem 0.6rem;
  border-radius: 999px;
  border: 1px solid rgba(233, 30, 140, 0.1);
}

.project-card__links {
  display: flex;
  gap: 0.8rem;
  margin-top: auto;
}

.project-link {
  font-family: 'Inter', sans-serif;
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--pink-hot);
  text-decoration: none;
  transition: all 0.2s ease;
  padding: 0.3rem 0.6rem;
  border-radius: 6px;
  background: rgba(233, 30, 140, 0.1);
  border: 1px solid transparent;
}

.project-link:hover {
  background: rgba(233, 30, 140, 0.2);
  border-color: var(--pink-hot);
  transform: translateY(-2px);
}

/* Carousel Buttons */
.carousel-btn {
  background: rgba(233, 30, 140, 0.1);
  border: 1px solid rgba(233, 30, 140, 0.3);
  border-radius: 50%;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: var(--pink-blush);
  transition: all 0.3s ease;
  flex-shrink: 0;
}

.carousel-btn:hover {
  background: rgba(233, 30, 140, 0.2);
  border-color: var(--pink-hot);
  color: var(--pink-hot);
  transform: scale(1.05);
}

/* Indicators */
.carousel-indicators {
  display: flex;
  justify-content: center;
  gap: 0.75rem;
  margin-top: 2rem;
  flex-wrap: wrap;
}

.indicator {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(244, 167, 195, 0.3);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  padding: 0;
}

.indicator:hover {
  background: rgba(244, 167, 195, 0.6);
}

.indicator.active {
  background: var(--pink-hot);
  width: 24px;
  border-radius: 10px;
}

/* ============================================ */
/* MODAL STYLES */
/* ============================================ */

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(26, 10, 15, 0.92);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 2rem;
  animation: modalFadeIn 0.3s ease;
}

.modal-content {
  background: var(--dark-base);
  border-radius: 24px;
  max-width: 700px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  border: 1px solid rgba(233, 30, 140, 0.2);
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.6);
  position: relative;
  animation: modalSlideUp 0.35s ease;
}

.modal-content::-webkit-scrollbar {
  width: 4px;
}

.modal-content::-webkit-scrollbar-thumb {
  background: var(--pink-hot);
  border-radius: 2px;
}

.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(233, 30, 140, 0.15);
  border: 1px solid rgba(233, 30, 140, 0.2);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: var(--pink-blush);
  transition: all 0.3s ease;
  z-index: 10;
}

.modal-close:hover {
  background: rgba(233, 30, 140, 0.3);
  border-color: var(--pink-hot);
  color: var(--pink-hot);
  transform: rotate(90deg);
}

.modal-image {
  width: 100%;
  height: 240px;
  overflow: hidden;
  border-radius: 24px 24px 0 0;
}

.modal-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-body {
  padding: 2rem;
}

.modal-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.8rem;
  color: var(--pink-pale);
  margin-bottom: 1rem;
}

.modal-description {
  font-family: 'Inter', sans-serif;
  font-size: 0.95rem;
  line-height: 1.8;
  color: rgba(244, 167, 195, 0.75);
  margin-bottom: 1.5rem;
  white-space: pre-wrap;
}

.modal-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.modal-tag {
  font-family: 'Inter', sans-serif;
  font-size: 0.7rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  background: rgba(233, 30, 140, 0.15);
  color: var(--pink-blush);
  padding: 0.3rem 0.8rem;
  border-radius: 999px;
  border: 1px solid rgba(233, 30, 140, 0.1);
}

.modal-links {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.modal-link {
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  font-weight: 600;
  text-decoration: none;
  padding: 0.7rem 1.5rem;
  border-radius: 999px;
  transition: all 0.3s ease;
}

.modal-link--primary {
  background: var(--pink-hot);
  color: #fff;
}

.modal-link--primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(233, 30, 140, 0.4);
}

.modal-link--secondary {
  color: var(--pink-blush);
  border: 1px solid rgba(244, 167, 195, 0.3);
}

.modal-link--secondary:hover {
  background: rgba(244, 167, 195, 0.06);
  border-color: rgba(244, 167, 195, 0.6);
  transform: translateY(-2px);
}

/* Modal Animations */
@keyframes modalFadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes modalSlideUp {
  from {
    opacity: 0;
    transform: translateY(30px) scale(0.96);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* Modal Transition */
.modal-enter-active {
  animation: modalFadeIn 0.3s ease;
}

.modal-leave-active {
  animation: modalFadeIn 0.25s ease reverse;
}

.modal-enter-active .modal-content {
  animation: modalSlideUp 0.35s ease;
}

.modal-leave-active .modal-content {
  animation: modalSlideUp 0.25s ease reverse;
}

/* Responsive */
@media (max-width: 900px) {
  .slide-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .projects__container {
    padding: calc(var(--header-h) + 2rem) 1.5rem 4rem;
  }
  .slide-grid {
    grid-template-columns: 1fr;
  }
  .carousel-btn {
    width: 36px;
    height: 36px;
  }
  .project-card {
    max-width: 100%;
  }
  
  .modal-content {
    max-width: 100%;
    margin: 1rem;
    max-height: 85vh;
  }
  
  .modal-image {
    height: 180px;
  }
  
  .modal-body {
    padding: 1.5rem;
  }
  
  .modal-title {
    font-size: 1.4rem;
  }
}
</style>