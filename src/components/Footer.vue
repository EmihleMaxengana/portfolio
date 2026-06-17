<template>
  <footer class="footer">
    <!-- REMOVED entire footer__main section with logo and navigation -->

    <!-- Bottom bar only -->
    <div class="footer__bar">
      <div class="footer__bar-inner">
        <p class="footer__copy">
          &copy; {{ year }} Emihle Maxengana. All rights reserved.
        </p>
        <div class="footer__socials">
          <a href="#" aria-label="GitHub" class="social__link">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/>
            </svg>
          </a>
          <a href="#" aria-label="LinkedIn" class="social__link">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
              <rect x="2" y="9" width="4" height="12"/>
              <circle cx="4" cy="4" r="2"/>
            </svg>
          </a>
          <a href="#" aria-label="Twitter / X" class="social__link">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"/>
            </svg>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  data() {
    return {
      year: new Date().getFullYear(),
    }
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
}

/* ── Footer shell ── */
.footer {
  background: var(--dark-base);
  border-top: 1px solid rgba(233, 30, 140, 0.18);
}

/* ── Bottom bar ── */
.footer__bar {
  padding: 1.5rem 0;
}

.footer__bar-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
}

.footer__copy {
  font-family: 'Inter', sans-serif;
  font-size: 0.8rem;
  color: rgba(244, 167, 195, 0.4);
  margin: 0;
}

/* ── Socials ── */
.footer__socials {
  display: flex;
  gap: 0.75rem;
}

.social__link {
  color: rgba(244, 167, 195, 0.45);
  transition: color 0.2s, transform 0.2s;
  display: flex;
  align-items: center;
}

.social__link:hover {
  color: var(--pink-hot);
  transform: translateY(-2px);
}

/* ── Responsive ── */
@media (max-width: 600px) {
  .footer__bar-inner {
    flex-direction: column;
    gap: 0.75rem;
    text-align: center;
  }
}
</style>