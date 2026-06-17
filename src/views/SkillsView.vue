<template>
  <main class="skills">
    <!-- Ambient orbs -->
    <div class="skills__orb skills__orb--1" aria-hidden="true"></div>
    <div class="skills__orb skills__orb--2" aria-hidden="true"></div>

    <div class="skills__container">
      <div class="skills__header">
        <!-- Glitched title -->
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
            <div v-for="(skill, index) in skills" :key="index" class="carousel-slide">
              <div class="skill-card">
                <div class="skill-card__image">
                  <img 
                    :src="skill.image" 
                    :alt="skill.label"
                    class="skill-img"
                  />
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
    </div>
  </main>
</template>

<script>
import canvaIcon from '@/assets/icons8-canva-24.png'
import cssIcon from '@/assets/icons8-css-24.png'
import dartIcon from '@/assets/icons8-dart-24.png'
import figmaIcon from '@/assets/icons8-figma-24.png'
import firebaseIcon from '@/assets/icons8-firebase-24.png'
import flutterIcon from '@/assets/icons8-flutter-24.png'
import htmlIcon from '@/assets/icons8-html5-24.png'
import javascriptIcon from '@/assets/icons8-javascript-24.png'
import mysqlIcon from '@/assets/icons8-mysql-24.png'
import oracleIcon from '@/assets/icons8-oracle-24.png'
import phpIcon from '@/assets/icons8-php-24.png'
import pythonIcon from '@/assets/icons8-python-24.png'
import reactIcon from '@/assets/icons8-react-24.png'
import vueIcon from '@/assets/icons8-vuejs-24.png'

export default {
  name: 'SkillsView',
  data() {
    return {
      currentIndex: 0,
      autoplayInterval: null,
      skills: [
        { image: canvaIcon, label: 'Canva' },
        { image: cssIcon, label: 'CSS' },
        { image: dartIcon, label: 'Dart' },
        { image: figmaIcon, label: 'Figma' },
        { image: firebaseIcon, label: 'Firebase' },
        { image: flutterIcon, label: 'Flutter' },
        { image: htmlIcon, label: 'HTML5' },
        { image: javascriptIcon, label: 'JavaScript' },
        { image: mysqlIcon, label: 'MySQL' },
        { image: oracleIcon, label: 'Oracle' },
        { image: phpIcon, label: 'PHP' },
        { image: pythonIcon, label: 'Python' },
        { image: reactIcon, label: 'React' },
        { image: vueIcon, label: 'Vue.js' }
      ]
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
      if (this.currentIndex < this.skills.length - 1) {
        this.currentIndex++
      } else {
        this.currentIndex = 0
      }
    },
    prevSlide() {
      if (this.currentIndex > 0) {
        this.currentIndex--
      } else {
        this.currentIndex = this.skills.length - 1
      }
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
  min-height: 100vh;
  overflow-x: hidden;
}

/* Ambient orbs */
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
  padding: calc(var(--header-h) + 3rem) 2rem 5rem;
  position: relative;
  z-index: 1;
}

/* Header */
.skills__header {
  text-align: center;
  margin-bottom: 4rem;
}

.skills__title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  margin-bottom: 1rem;
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

/* Glitch effect */
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

/* Carousel Styles */
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
  max-width: 900px;
  margin: 0 1rem;
}

.carousel-track {
  display: flex;
  transition: transform 0.5s ease-in-out;
}

.carousel-slide {
  flex: 0 0 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

/* Skill Card */
.skill-card {
  background: rgba(233, 30, 140, 0.05);
  border-radius: 24px;
  padding: 2rem;
  text-align: center;
  border: 1px solid rgba(233, 30, 140, 0.2);
  transition: all 0.3s ease;
  width: 100%;
  max-width: 300px;
  margin: 0 auto;
}

.skill-card:hover {
  border-color: rgba(233, 30, 140, 0.5);
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(233, 30, 140, 0.1);
}

.skill-card__image {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.skill-img {
  width: 80px;
  height: 80px;
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
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--pink-blush);
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

/* Responsive */
@media (max-width: 768px) {
  .skills__container {
    padding: calc(var(--header-h) + 2rem) 1.5rem 4rem;
  }
  
  .carousel-btn {
    width: 36px;
    height: 36px;
  }
  
  .skill-card {
    padding: 1.5rem;
  }
  
  .skill-img {
    width: 60px;
    height: 60px;
  }
  
  .skill-card__label {
    font-size: 0.9rem;
  }
}

@media (max-width: 600px) {
  .carousel-container {
    margin: 1rem 0;
  }
  
  .carousel-btn {
    width: 32px;
    height: 32px;
  }
  
  .carousel-btn svg {
    width: 18px;
    height: 18px;
  }
  
  .skill-img {
    width: 50px;
    height: 50px;
  }
}
</style>