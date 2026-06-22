<template>
  <footer class="footer">
    <div class="footer__bar">
      <div class="footer__bar-inner">
        <p class="footer__copy">
          &copy; {{ year }} Emihle Maxengana. All rights reserved.
        </p>
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