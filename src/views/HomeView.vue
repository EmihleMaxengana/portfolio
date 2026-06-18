<template>
  <main class="home">
    <!-- ── Hero ── -->
    <section class="hero">
      <div class="hero__orb hero__orb--1" aria-hidden="true"></div>
      <div class="hero__orb hero__orb--2" aria-hidden="true"></div>

      <div class="hero__container">
        <div class="hero__content">
          
          <!-- GLITCHED NAME - straight line on desktop, stacks on mobile -->
          <h1 class="hero__name glitch-text" data-text="Emihle Maxengana">
            Emihle Maxengana
          </h1>

          <!-- ROTATING ROLES -->
          <div class="hero__roles">
            <span class="roles__rotating">{{ currentRole }}</span>
          </div>

           <p class="hero__bio">
            Crafting complete applications that look great and perform even better
          </p>
          <p class="hero__bio">
            Where creativity meets code.
          </p>
          <p class="hero__bio">
            Powering applications behind the scenes.
          </p>
          <p class="hero__bio">
           Building mobile experiences that make an impact.
          </p>

          <div class="hero__actions">
            <router-link to="/projects" class="btn btn--primary">View My Work</router-link>
            <router-link to="/contact" class="btn btn--ghost">Get In Touch</router-link>
          </div>

          <div class="hero__scroll" aria-hidden="true">
            <span class="scroll__label">scroll</span>
            <span class="scroll__line"></span>
          </div>
        </div>

        <div class="hero__image">
          <div class="image__wrapper">
            <img 
              :src="profileImage"
              alt="Emihle Maxengana"
              class="profile__img"
            />
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
// IMPORT your image here
import profileImage from '@/assets/EmihleHomePage.png'

export default {
  name: 'HomeView',
  data() {
    return {
      profileImage, // Add this to data
      roles: [
        'Frontend Developer',
        'Backend Developer', 
        'Full Stack Developer',
        'Mobile Developer',
        'UI/UX Designer'
      ],
      currentRoleIndex: 0,
      currentRole: 'Frontend Developer'
    }
  },
  mounted() {
    setInterval(() => {
      this.currentRoleIndex = (this.currentRoleIndex + 1) % this.roles.length
      this.currentRole = this.roles[this.currentRoleIndex]
    }, 1800)
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
  --dark-mid: #3d1a27;
  --header-h: 72px;
}

.home {
  background: var(--dark-base);
  min-height: 100vh;
  overflow-x: hidden;
}

.hero {
  position: relative;
  min-height: 100vh;
  padding: calc(var(--header-h) + 2rem) 2rem 4rem;
  max-width: 1200px;
  margin: 0 auto;
}

.hero__container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 4rem;
  flex-wrap: wrap;
}

.hero__content {
  position: relative;
  z-index: 1;
  flex: 1;
  min-width: 280px;
}

.hero__image {
  flex: 1;
  display: flex;
  justify-content: center;
  animation: fadeUp 0.7s 0.4s ease both;
}

.image__wrapper {
  width: 100%;
  max-width: 380px;
  border-radius: 30px;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 0 1px rgba(233,30,140,0.2);
}

.profile__img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.4s ease;
}

.profile__img:hover {
  transform: scale(1.02);
}

.hero__orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
}

.hero__orb--1 {
  width: 500px;
  height: 500px;
  background: rgba(233, 30, 140, 0.12);
  top: -100px;
  left: -200px;
}

.hero__orb--2 {
  width: 360px;
  height: 360px;
  background: rgba(244, 167, 195, 0.07);
  bottom: 60px;
  right: -100px;
}

/* GLITCHED NAME - straight line on desktop, half font size */
.hero__name {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.8rem, 5vw, 2.5rem);
  font-weight: 700;
  margin: 0 0 1rem;
  color: var(--pink-hot);
  position: relative;
  display: inline-block;
  animation: glitch-skew 3s infinite ease-in-out;
  line-height: 1.2;
  white-space: nowrap;
}

/* On smaller devices, allow stacking */
@media (max-width: 500px) {
  .hero__name {
    white-space: normal;
    text-align: center;
    display: block;
    font-size: clamp(1.5rem, 7vw, 2rem);
  }
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

/* ROTATING ROLES - doubled size */
.hero__roles {
  font-family: 'Inter', sans-serif;
  font-size: clamp(2rem, 6vw, 3rem);
  margin-bottom: 1.5rem;
  color: rgba(244, 167, 195, 0.9);
  font-weight: 500;
}

.roles__prefix {
  margin-right: 0.75rem;
}

.roles__rotating {
  color: var(--pink-hot);
  font-weight: 700;
  display: inline-block;
  animation: fadeSlide 0.5s ease-out;
}

@keyframes fadeSlide {
  0% {
    opacity: 0;
    transform: translateY(10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero__bio {
  font-family: 'Inter', sans-serif;
  font-size: clamp(1rem, 2vw, 1.15rem);
  line-height: 1.75;
  color: rgba(244, 167, 195, 0.75);
  max-width: 520px;
  margin: 0 0 2.5rem;
  animation: fadeUp 0.7s 0.3s ease both;
}

.hero__actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  animation: fadeUp 0.7s 0.4s ease both;
}

.btn {
  font-family: 'Inter', sans-serif;
  font-size: 0.9rem;
  font-weight: 600;
  text-decoration: none;
  padding: 0.85rem 2rem;
  border-radius: 999px;
  transition: transform 0.2s, opacity 0.2s, box-shadow 0.2s;
  display: inline-block;
}

.btn--primary {
  background: var(--pink-hot);
  color: #fff;
  box-shadow: 0 0 30px rgba(233, 30, 140, 0.35);
}

.btn--primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 40px rgba(233, 30, 140, 0.5);
}

.btn--ghost {
  color: var(--pink-blush);
  border: 1px solid rgba(244, 167, 195, 0.3);
}

.btn--ghost:hover {
  background: rgba(244, 167, 195, 0.06);
  transform: translateY(-2px);
  border-color: rgba(244, 167, 195, 0.6);
}

.hero__scroll {
  position: absolute;
  bottom: 2.5rem;
  left: 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  animation: fadeUp 0.7s 0.7s ease both;
}

.scroll__label {
  font-family: 'Inter', sans-serif;
  font-size: 0.65rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: rgba(244, 167, 195, 0.35);
  writing-mode: vertical-lr;
}

.scroll__line {
  width: 1px;
  height: 60px;
  background: linear-gradient(to bottom, rgba(233, 30, 140, 0.6), transparent);
  animation: scrollPulse 2s ease-in-out infinite;
}

@keyframes scrollPulse {
  0%, 100% { opacity: 0.3; transform: scaleY(0.7); }
  50% { opacity: 1; transform: scaleY(1); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 900px) {
  .hero__container {
    flex-direction: column;
    text-align: center;
  }
  
  .hero__bio {
    margin-left: auto;
    margin-right: auto;
  }
  
  .hero__actions {
    justify-content: center;
  }
  
  .hero__scroll {
    left: 50%;
    transform: translateX(-50%);
  }
}

@media (max-width: 600px) {
  .hero {
    padding-top: calc(var(--header-h) + 1rem);
  }

  .hero__actions {
    flex-direction: column;
    align-items: center;
  }

  .btn {
    text-align: center;
    width: 200px;
  }
  
  .image__wrapper {
    max-width: 280px;
  }
}
</style>