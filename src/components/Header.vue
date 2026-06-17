<template>
  <header class="header" :class="{ scrolled: isScrolled }">
    <div class="header__inner">
      <!-- Logo -->
      <router-link to="/" class="header__logo">
        <span class="logo__mark">E</span>
        <span class="logo__name">Emihle</span>
      </router-link>

      <!-- Desktop Nav -->
      <nav class="header__nav" aria-label="Main navigation">
        <router-link
          v-for="link in navLinks"
          :key="link.to"
          :to="link.to"
          class="nav__link"
          active-class="nav__link--active"
        >
          {{ link.label }}
        </router-link>
        <a href="#contact" class="nav__cta">Let's Talk</a>
      </nav>

      <!-- Mobile Hamburger -->
      <button
        class="header__burger"
        :class="{ open: menuOpen }"
        @click="menuOpen = !menuOpen"
        aria-label="Toggle menu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>

    <!-- Mobile Drawer -->
    <transition name="drawer">
      <div v-if="menuOpen" class="header__drawer">
        <router-link
          v-for="link in navLinks"
          :key="link.to"
          :to="link.to"
          class="drawer__link"
          active-class="drawer__link--active"
          @click="menuOpen = false"
        >
          {{ link.label }}
        </router-link>
        <a href="#contact" class="drawer__cta" @click="menuOpen = false">Let's Talk</a>
      </div>
    </transition>
  </header>
</template>

<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      isScrolled: false,
      menuOpen: false,
      navLinks: [
        { to: '/', label: 'Home' },
        { to: '/about', label: 'About' },
        { to: '/skills', label: 'Skills' },
        { to: '/projects', label: 'Projects' },
        { to: '/contact', label: 'Contact' },
      ],
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 40
    },
  },
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Inter:wght@400;500;600&display=swap');

/* ── Variables ── */
:root {
  --pink-hot: #e91e8c;
  --pink-blush: #f4a7c3;
  --pink-pale: #fdf0f5;
  --dark-base: #1a0a0f;
  --dark-mid: #3d1a27;
  --header-h: 72px;
}

/* ── Header shell ── */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  height: var(--header-h);
  transition: background 0.3s ease, box-shadow 0.3s ease;
  background: transparent;
}

.header.scrolled {
  background: rgba(26, 10, 15, 0.82);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  box-shadow: 0 1px 0 rgba(233, 30, 140, 0.15);
}

.header__inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* ── Logo ── */
.header__logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  text-decoration: none;
  font-family: 'Playfair Display', serif;
}

.logo__mark {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: var(--pink-hot);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  font-weight: 700;
  letter-spacing: 0;
  flex-shrink: 0;
}

.logo__name {
  font-size: 1.25rem;
  color: var(--pink-pale);
  font-weight: 700;
  letter-spacing: 0.02em;
}

/* ── Desktop nav ── */
.header__nav {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.nav__link {
  font-family: 'Inter', sans-serif;
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--pink-blush);
  text-decoration: none;
  padding: 0.4rem 0.85rem;
  border-radius: 6px;
  transition: color 0.2s, background 0.2s;
  letter-spacing: 0.03em;
}

.nav__link:hover,
.nav__link--active {
  color: #fff;
  background: rgba(233, 30, 140, 0.12);
}

.nav__link--active {
  color: var(--pink-hot);
}

.nav__cta {
  font-family: 'Inter', sans-serif;
  font-size: 0.875rem;
  font-weight: 600;
  color: #fff;
  text-decoration: none;
  padding: 0.5rem 1.25rem;
  border-radius: 999px;
  background: var(--pink-hot);
  margin-left: 0.75rem;
  transition: opacity 0.2s, transform 0.2s;
}

.nav__cta:hover {
  opacity: 0.88;
  transform: translateY(-1px);
}

/* ── Burger ── */
.header__burger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}

.header__burger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--pink-blush);
  border-radius: 2px;
  transition: transform 0.3s, opacity 0.3s;
}

.header__burger.open span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}
.header__burger.open span:nth-child(2) {
  opacity: 0;
}
.header__burger.open span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

/* ── Drawer ── */
.header__drawer {
  position: absolute;
  top: var(--header-h);
  left: 0;
  right: 0;
  background: rgba(26, 10, 15, 0.97);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  padding: 1.5rem 2rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  border-top: 1px solid rgba(233, 30, 140, 0.2);
}

.drawer__link {
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  color: var(--pink-blush);
  text-decoration: none;
  padding: 0.75rem 0;
  border-bottom: 1px solid rgba(244, 167, 195, 0.1);
  transition: color 0.2s;
}

.drawer__link:hover,
.drawer__link--active {
  color: var(--pink-hot);
}

.drawer__cta {
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  font-weight: 600;
  color: #fff;
  text-decoration: none;
  padding: 0.85rem 1.5rem;
  border-radius: 999px;
  background: var(--pink-hot);
  text-align: center;
  margin-top: 1rem;
  transition: opacity 0.2s;
}

.drawer__cta:hover {
  opacity: 0.88;
}

/* ── Transition ── */
.drawer-enter-active,
.drawer-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}
.drawer-enter-from,
.drawer-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .header__nav {
    display: none;
  }
  .header__burger {
    display: flex;
  }
}
</style>