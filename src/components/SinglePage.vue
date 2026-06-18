<template>
  <main>
    <section id="home">
      <HomeView />
    </section>
    <section id="about">
      <AboutView />
    </section>
    <section id="skills">
      <SkillsView />
    </section>
    <section id="projects">
      <ProjectsView />
    </section>
    <section id="contact">
      <ContactView />
    </section>
  </main>
</template>

<script>
import HomeView from '@/views/HomeView.vue'
import AboutView from '@/views/AboutView.vue'
import SkillsView from '@/views/SkillsView.vue'
import ProjectsView from '@/views/ProjectsView.vue'
import ContactView from '@/views/ContactView.vue'

export default {
  name: 'SinglePage',
  components: {
    HomeView,
    AboutView,
    SkillsView,
    ProjectsView,
    ContactView,
  },
}
</script>

<style scoped>
section {
  scroll-margin-top: var(--header-h, 72px);
}
</style>