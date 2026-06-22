<template>
  <main class="about">
    <div class="about__orb about__orb--1" aria-hidden="true"></div>
    <div class="about__orb about__orb--2" aria-hidden="true"></div>

    <div class="about__container">
      <div class="about__grid">
        <div class="about__image">
          <div class="image__wrapper">
            <img 
              :src="profileImage"
              alt="Emihle Maxengana"
              class="about__img"
            />
          </div>
        </div>

        <div class="about__content">
          <h1 class="about__title glitch-text" data-text="About Me">
            About Me
          </h1>

          <p class="about__bio">
            Creative and results-driven Full-Stack Developer with experience designing and building modern web and mobile applications using a variety of programming languages, frameworks, and development tools.
          </p>
          <p class="about__bio">
            Passionate about crafting responsive, high-performance, and user-centered digital solutions that seamlessly blend functionality, scalability, and intuitive design. Skilled in both front-end and back-end development, with a strong focus on clean code, problem-solving, and delivering exceptional user experiences.
          </p>
          <p class="about__bio">
            Recognized for adaptability, attention to detail, and a commitment to continuous learning, with the ability to thrive in fast-paced and collaborative environments. Eager to contribute innovative ideas, technical expertise, and a strong work ethic to forward-thinking organizations.
          </p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import profileImage from '@/assets/EmihleAboutPage.jpg'

export default {
  name: 'AboutView',
  data() {
    return {
      profileImage,
    }
  },
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,700&family=Inter:wght@400;500;600&display=swap');

:root {
  --pink-hot: #e91e8c;
  --pink-blush: #f4a7c3;
  --pink-pale: #fdf0f5;
  --dark-base: #1a0a0f;
  --dark-mid: #3d1a27;
  --header-h: 72px;
}

.about {
  background: var(--dark-base);
  min-height: 100vh;
  overflow-x: hidden;
}

/* Ambient orbs */
.about__orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
}

.about__orb--1 {
  width: 500px;
  height: 500px;
  background: rgba(233, 30, 140, 0.12);
  top: -100px;
  left: -200px;
}

.about__orb--2 {
  width: 360px;
  height: 360px;
  background: rgba(244, 167, 195, 0.07);
  bottom: 60px;
  right: -100px;
}

.about__container {
  max-width: 1200px;
  margin: 0 auto;
  padding: calc(var(--header-h) + 1.5rem) 2rem 3rem;;
  position: relative;
  z-index: 1;
}

/* Two column grid layout */
.about__grid {
  display: flex;
  align-items: center;
  gap: 4rem;
  flex-wrap: wrap;
}

/* Left side - Image */
.about__image {
  flex: 1;
  min-width: 280px;
  display: flex;
  justify-content: center;
}

.image__wrapper {
  width: 100%;
  max-width: 400px;
  border-radius: 30px;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 0 1px rgba(233,30,140,0.2);
}

.about__img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.4s ease;
}

.about__img:hover {
  transform: scale(1.02);
}

/* Right side - Content */
.about__content {
  flex: 1;
  min-width: 280px;
}

/* Glitched title */
.about__title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  margin-bottom: 2rem;
  color: var(--pink-hot);
  position: relative;
  display: inline-block;
  animation: glitch-skew 3s infinite ease-in-out;
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

/* Bio text */
.about__bio {
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  line-height: 1.8;
  color: rgba(244, 167, 195, 0.75);
  margin-bottom: 1.5rem;
  animation: fadeUp 0.5s ease both;
}

.about__bio:nth-child(2) { animation-delay: 0.1s; }
.about__bio:nth-child(3) { animation-delay: 0.2s; }
.about__bio:nth-child(4) { animation-delay: 0.3s; }

/* Animations */
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive - stacks on mobile */
@media (max-width: 900px) {
  .about__grid {
    flex-direction: column;
    text-align: center;
    gap: 2rem;
  }
  
  .about__content {
    text-align: center;
  }
}

@media (max-width: 600px) {
  .about__container {
    padding: calc(var(--header-h) + 2rem) 1.5rem 4rem;
  }
  
  .image__wrapper {
    max-width: 280px;
  }
}
</style>