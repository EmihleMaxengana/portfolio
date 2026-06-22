<template>
  <main class="skills">
    <!-- Ambient orbs -->
    <div class="skills__orb skills__orb--1" aria-hidden="true"></div>
    <div class="skills__orb skills__orb--2" aria-hidden="true"></div>

    <div class="skills__container">
      <div class="skills__header">
        <h1 class="skills__title glitch-text" data-text="Skills & Technologies">
          Skills & Technologies
        </h1>
        <p class="skills__subtitle">Technologies I work with</p>
      </div>

      <!-- Image Carousel -->
      <div 
        class="carousel-container" 
        @mouseenter="stopAutoplay" 
        @mouseleave="startAutoplay"
      >
        <button class="carousel-btn prev-btn" @click="prevSlide" aria-label="Previous">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M15 18l-6-6 6-6"/>
          </svg>
        </button>

        <div class="carousel-wrapper">
          <div class="carousel-track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
            <div v-for="(chunk, slideIndex) in skillChunks" :key="slideIndex" class="carousel-slide">
              <div class="slide-grid">
                <div v-for="skill in chunk" :key="skill.label" class="skill-card">
                  <div class="skill-card__image">
                    <img 
                      :src="skill.image" 
                      :alt="skill.label"
                      class="skill-img"
                    />
                  </div>
                  <span class="skill-card__label">{{ skill.label }}</span>
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

      <!-- Indicators -->
      <div class="carousel-indicators">
        <button 
          v-for="(_, index) in skillChunks" 
          :key="index"
          @click="goToSlide(index)"
          class="indicator"
          :class="{ active: currentIndex === index }"
          :aria-label="`Go to slide ${index + 1}`"
        ></button>
      </div>
    </div>
  </main>
</template>

<script>
import canvaIcon from '@/assets/Canva.jpg'
import cssIcon from '@/assets/CSS.png'
import dartIcon from '@/assets/dart.jpg'
import figmaIcon from '@/assets/Figma.jpg'
import firebaseIcon from '@/assets/Firebase.jpg'
import flutterIcon from '@/assets/Flutter.jpg'
import htmlIcon from '@/assets/HTML5.png'
import javascriptIcon from '@/assets/javascript.jpg'
import mysqlIcon from '@/assets/mysql.png'
import oracleIcon from '@/assets/oracle.jpg'
import phpIcon from '@/assets/php.jpg'
import pythonIcon from '@/assets/python.png'
import reactIcon from '@/assets/react.png'
import vueIcon from '@/assets/vue.jpg'

export default {
  name: 'SkillsView',
  data() {
    return {
      currentIndex: 0,
      autoplayInterval: null,
      skills: [
        { image: vueIcon, label: 'Vue.js' },
        { image: reactIcon, label: 'React' },
        { image: oracleIcon, label: 'Oracle' },
        { image: phpIcon, label: 'PHP' },
        { image: pythonIcon, label: 'Python' },
        { image: mysqlIcon, label: 'MySQL' },
        { image: javascriptIcon, label: 'JavaScript' },
        { image: htmlIcon, label: 'HTML5' },
        { image: firebaseIcon, label: 'Firebase' },
        { image: flutterIcon, label: 'Flutter' },
        { image: figmaIcon, label: 'Figma' },
        { image: cssIcon, label: 'CSS' },
        { image: canvaIcon, label: 'Canva' },
        { image: dartIcon, label: 'Dart' }
      ]
    }
  },
  computed: {
    skillChunks() {
      const chunkSize = 3
      const chunks = []
      for (let i = 0; i < this.skills.length; i += chunkSize) {
        chunks.push(this.skills.slice(i, i + chunkSize))
      }
      return chunks
    }
  },
  mounted() {
    this.startAutoplay()
  },
  beforeUnmount() {
    this.stopAutoplay()
  },
  methods: {
    nextSlide() {
      if (this.currentIndex < this.skillChunks.length - 1) {
        this.currentIndex++
      } else {
        this.currentIndex = 0
      }
    },
    prevSlide() {
      if (this.currentIndex > 0) {
        this.currentIndex--
      } else {
        this.currentIndex = this.skillChunks.length - 1
      }
    },
    goToSlide(index) {
      this.currentIndex = index
    },
    startAutoplay() {
      if (this.autoplayInterval) return
      this.autoplayInterval = setInterval(() => {
        this.nextSlide()
      }, 2500)
    },
    stopAutoplay() {
      if (this.autoplayInterval) {
        clearInterval(this.autoplayInterval)
        this.autoplayInterval = null
      }
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

.skills {
  background: var(--dark-base);
  /* REMOVED min-height: 100vh – no more forced full viewport height */
  overflow-x: hidden;
}

.skills__orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
}

.skills__orb--1 {
  width: 500px;
  height: 500px;
  background: rgba(233, 30, 140, 0.12);
  top: -100px;
  left: -200px;
}

.skills__orb--2 {
  width: 360px;
  height: 360px;
  background: rgba(244, 167, 195, 0.07);
  bottom: 60px;
  right: -100px;
}

.skills__container {
  max-width: 1200px;
  margin: 0 auto;
  /* MINIMAL bottom padding – just a tiny gap before footer */
  padding: calc(var(--header-h) + 1.5rem) 2rem 0.5rem;
  position: relative;
  z-index: 1;
}

.skills__header {
  text-align: center;
  margin-bottom: 1.5rem; /* reduced from 2rem */
}

.skills__title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: var(--pink-hot);
  position: relative;
  display: inline-block;
  animation: glitch-skew 3s infinite ease-in-out;
}

.skills__subtitle {
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
  margin: 1rem 0 0.25rem 0; /* minimal margins */
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
  padding: 0.5rem 0; /* reduced from 1rem */
}

.slide-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem; /* reduced from 1.5rem */
  justify-items: center;
}

.skill-card {
  background: rgba(233, 30, 140, 0.05);
  border-radius: 24px;
  padding: 1rem; /* reduced from 1.5rem */
  text-align: center;
  border: 1px solid rgba(233, 30, 140, 0.2);
  transition: all 0.3s ease;
  width: 100%;
  max-width: 180px; /* slightly smaller */
  margin: 0 auto;
}

.skill-card:hover {
  border-color: rgba(233, 30, 140, 0.5);
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(233, 30, 140, 0.1);
}

.skill-card__image {
  display: flex;
  justify-content: center;
  margin-bottom: 0.5rem; /* reduced */
}

.skill-img {
  width: 60px; /* reduced from 70px */
  height: 60px;
  object-fit: contain;
  filter: brightness(0.9) drop-shadow(0 0 5px rgba(233, 30, 140, 0.3));
  transition: all 0.3s ease;
}

.skill-card:hover .skill-img {
  filter: brightness(1) drop-shadow(0 0 10px rgba(233, 30, 140, 0.5));
  transform: scale(1.05);
}

.skill-card__label {
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem; /* slightly smaller */
  font-weight: 600;
  color: var(--pink-blush);
}

.carousel-btn {
  background: rgba(233, 30, 140, 0.1);
  border: 1px solid rgba(233, 30, 140, 0.3);
  border-radius: 50%;
  width: 40px; /* reduced from 48px */
  height: 40px;
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

.carousel-indicators {
  display: flex;
  justify-content: center;
  gap: 0.5rem; /* reduced */
  margin-top: 0.25rem; /* almost nothing */
  flex-wrap: wrap;
}

.indicator {
  width: 8px; /* reduced */
  height: 8px;
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
  width: 20px; /* reduced */
  border-radius: 10px;
}

@media (max-width: 900px) {
  .slide-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .skills__container {
    padding: calc(var(--header-h) + 1.5rem) 1.5rem 0.5rem;
  }
  .slide-grid {
    grid-template-columns: 1fr;
  }
  .carousel-btn {
    width: 32px;
    height: 32px;
  }
  .skill-card {
    max-width: 100%;
  }
}
</style>