<template>
  <main class="contact">
    <!-- Ambient orbs -->
    <div class="contact__orb contact__orb--1" aria-hidden="true"></div>
    <div class="contact__orb contact__orb--2" aria-hidden="true"></div>

    <div class="contact__container">
      <div class="contact__header">
        <!-- Glitched title -->
        <h1 class="contact__title glitch-text" data-text="Contact">
          Contact
        </h1>
        <p class="contact__subtitle">Get in touch with me</p>
      </div>

      <!-- Bio at the top after subtitle - NO BORDER -->
      <div class="contact__bio-section">
        <p class="contact__bio">
          I am currently open to professional opportunities, internships, and freelance collaborations. 
          With a strong foundation in full-stack development and a passion for creating impactful 
          digital solutions, I am eager to contribute my skills to innovative projects and forward-thinking teams. 
          If you are looking for a dedicated, adaptable, and results-oriented developer, I would welcome 
          the opportunity to connect. Please feel free to reach out through the contact information below 
          to discuss potential collaborations or opportunities.
        </p>
      </div>

      <div class="contact__grid">
        <!-- Left side - Contact info -->
        <div class="contact__left">
          <div class="contact__info">
            <h3 class="contact__info-title">Contact Information</h3>
            
            <div class="contact__details">
              <!-- Fixed mailto link -->
              <a href="mailto:emihlemaxengana05@gmail.com?subject=Portfolio%20Inquiry&body=Hello%20Emihle%2C%0A%0AI%20came%20across%20your%20portfolio%20and%20would%20like%20to%20get%20in%20touch%20with%20you.%0A%0A" class="contact-detail">
                <svg class="detail-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
                <span>emihlemaxengana05@gmail.com</span>
              </a>
              
              <!-- Fixed tel link -->
              <a href="tel:+27710053360" class="contact-detail">
                <svg class="detail-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.127.96.362 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.338 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/>
                </svg>
                <span>071 005 3360</span>
              </a>
              
              <!-- LinkedIn opens in new tab -->
              <a href="https://www.linkedin.com/in/emihle-maxengana-82561b327" target="_blank" rel="noopener noreferrer" class="contact-detail">
                <svg class="detail-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
                  <rect x="2" y="9" width="4" height="12"/>
                  <circle cx="4" cy="4" r="2"/>
                </svg>
                <span>LinkedIn Profile</span>
              </a>
              
              <!-- GitHub opens in new tab -->
              <a href="https://github.com/EmihleMaxengana" target="_blank" rel="noopener noreferrer" class="contact-detail">
                <svg class="detail-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"/>
                </svg>
                <span>GitHub Profile</span>
              </a>
            </div>
          </div>
        </div>

        <!-- Right side - Contact Form -->
        <div class="contact__right">
          <form @submit.prevent="handleSubmit" class="contact-form">
            <div class="form-group">
              <label for="name">Name</label>
              <input 
                type="text" 
                id="name" 
                v-model="form.name"
                placeholder="Enter your name"
                required
              />
            </div>

            <div class="form-group">
              <label for="phone">Phone Number</label>
              <input 
                type="tel" 
                id="phone" 
                v-model="form.phone"
                placeholder="Enter your phone number"
              />
            </div>

            <div class="form-group">
              <label for="email">Email Address</label>
              <input 
                type="email" 
                id="email" 
                v-model="form.email"
                placeholder="Enter your email"
                required
              />
            </div>

            <div class="form-group">
              <label for="message">Message</label>
              <textarea 
                id="message" 
                v-model="form.message"
                rows="5"
                placeholder="Write your message here"
                required
              ></textarea>
            </div>

            <button type="submit" class="submit-btn">Send Message</button>
          </form>

          <!-- Success Message -->
          <div v-if="showSuccess" class="success-message">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
              <polyline points="22 4 12 14.01 9 11.01"/>
            </svg>
            <span>Message sent successfully! I'll get back to you soon.</span>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'ContactView',
  data() {
    return {
      form: {
        name: '',
        phone: '',
        email: '',
        message: ''
      },
      showSuccess: false
    }
  },
  methods: {
    handleSubmit() {
      // Open email client with form data pre-filled
      const subject = encodeURIComponent(`Portfolio Inquiry from ${this.form.name || 'Visitor'}`)
      const body = encodeURIComponent(
        `Name: ${this.form.name}\n` +
        `Phone: ${this.form.phone || 'Not provided'}\n` +
        `Email: ${this.form.email}\n\n` +
        `Message:\n${this.form.message}\n\n` +
        `---\nSent from your portfolio website`
      )
      
      // Create mailto link and open it
      const mailtoLink = `mailto:emihlemaxengana05@gmail.com?subject=${subject}&body=${body}`
      window.location.href = mailtoLink
      
      // Show success message
      this.showSuccess = true
      
      // Reset form
      this.form = {
        name: '',
        phone: '',
        email: '',
        message: ''
      }
      
      // Hide success message after 5 seconds
      setTimeout(() => {
        this.showSuccess = false
      }, 5000)
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

.contact {
  background: var(--dark-base);
  min-height: 100vh;
  overflow-x: hidden;
}

/* Ambient orbs */
.contact__orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
}

.contact__orb--1 {
  width: 500px;
  height: 500px;
  background: rgba(233, 30, 140, 0.12);
  top: -100px;
  left: -200px;
}

.contact__orb--2 {
  width: 360px;
  height: 360px;
  background: rgba(244, 167, 195, 0.07);
  bottom: 60px;
  right: -100px;
}

.contact__container {
  max-width: 1200px;
  margin: 0 auto;
  padding: calc(var(--header-h) + 3rem) 2rem 5rem;
  position: relative;
  z-index: 1;
}

/* Header */
.contact__header {
  text-align: center;
  margin-bottom: 2rem;
}

.contact__title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: var(--pink-hot);
  position: relative;
  display: inline-block;
  animation: glitch-skew 3s infinite ease-in-out;
}

.contact__subtitle {
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  color: rgba(244, 167, 195, 0.6);
  letter-spacing: 0.05em;
}

/* Bio Section - at the top - NO BORDER */
.contact__bio-section {
  max-width: 900px;
  margin: 0 auto 3rem auto;
}

.contact__bio {
  font-family: 'Inter', sans-serif;
  font-size: 0.95rem;
  line-height: 1.8;
  color: rgba(244, 167, 195, 0.75);
  text-align: center;
  background: transparent;
  padding: 0;
  border: none;
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

/* Two column grid layout */
.contact__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
}

/* Left side - Info */
.contact__left {
  background: rgba(233, 30, 140, 0.05);
  border-radius: 24px;
  padding: 2rem;
  border: 1px solid rgba(233, 30, 140, 0.15);
}

.contact__info-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--pink-hot);
  margin-bottom: 1.5rem;
}

.contact__details {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.contact-detail {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  color: rgba(244, 167, 195, 0.7);
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 0.5rem;
  border-radius: 12px;
}

.contact-detail:hover {
  background: rgba(233, 30, 140, 0.1);
  color: var(--pink-hot);
  transform: translateX(5px);
}

.contact-detail:hover .detail-icon {
  color: var(--pink-hot);
}

.detail-icon {
  color: rgba(244, 167, 195, 0.6);
  flex-shrink: 0;
  transition: color 0.3s ease;
}

/* Right side - Form */
.contact__right {
  background: rgba(233, 30, 140, 0.05);
  border-radius: 24px;
  padding: 2rem;
  border: 1px solid rgba(233, 30, 140, 0.15);
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--pink-blush);
  letter-spacing: 0.03em;
}

.form-group input,
.form-group textarea {
  background: rgba(233, 30, 140, 0.1);
  border: 1px solid rgba(233, 30, 140, 0.2);
  border-radius: 12px;
  padding: 0.85rem 1rem;
  font-family: 'Inter', sans-serif;
  font-size: 0.9rem;
  color: var(--pink-pale);
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--pink-hot);
  background: rgba(233, 30, 140, 0.15);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(244, 167, 195, 0.4);
}

.submit-btn {
  background: var(--pink-hot);
  color: white;
  font-family: 'Inter', sans-serif;
  font-size: 0.9rem;
  font-weight: 600;
  padding: 0.85rem 2rem;
  border: none;
  border-radius: 999px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 0.5rem;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(233, 30, 140, 0.4);
}

.success-message {
  margin-top: 1.5rem;
  padding: 1rem;
  background: rgba(233, 30, 140, 0.15);
  border: 1px solid rgba(233, 30, 140, 0.3);
  border-radius: 12px;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: var(--pink-blush);
  font-family: 'Inter', sans-serif;
  font-size: 0.85rem;
  animation: fadeUp 0.3s ease;
}

.success-message svg {
  color: var(--pink-hot);
  flex-shrink: 0;
}

/* Animations */
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive */
@media (max-width: 900px) {
  .contact__grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .contact__bio {
    font-size: 0.85rem;
  }
}

@media (max-width: 600px) {
  .contact__container {
    padding: calc(var(--header-h) + 2rem) 1.5rem 4rem;
  }
  
  .contact__left,
  .contact__right {
    padding: 1.5rem;
  }
  
  .contact-detail {
    font-size: 0.75rem;
  }
  
  .submit-btn {
    width: 100%;
  }
  
  .contact__bio {
    font-size: 0.8rem;
  }
}
</style>