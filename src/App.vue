<template>
  <div id="app" class="cyber-container">
    <div class="scanline"></div>
    <header class="glitch-header">
      <h1>SHIVAM DUBEY</h1>
      <p class="subtitle">Software Engineer | Frontend & Backend Architecture</p>
    </header>
    
    <main>
      <HeroSection />
      <ExperienceSection />
      <ProjectsSection />
      <SkillsSection />
      <ContactsSection />
    </main>

  </div>
</template>

<script setup>
import HeroSection from './components/HeroSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ContactsSection from './components/ContactsSection.vue';
</script>

<style>
:root {
  --neon-cyan: #00f0ff;
  --neon-purple: #b026ff;
  --dark-bg: #0a0a0f;
  --panel-bg: rgba(10, 10, 15, 0.85);
}

body {
  margin: 0;
  background-color: var(--dark-bg);
  color: #fff;
  font-family: 'Courier New', Courier, monospace;
  background-image: linear-gradient(rgba(0, 240, 255, 0.05) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(0, 240, 255, 0.05) 1px, transparent 1px);
  background-size: 30px 30px;
}

.cyber-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  position: relative;
}

.scanline {
  width: 100%;
  height: 100px;
  background: linear-gradient(0deg, transparent, rgba(0, 240, 255, 0.2), transparent);
  position: fixed;
  top: -100px;
  animation: scan 4s infinite linear;
  pointer-events: none;
  z-index: 9999;
}

@keyframes scan {
  0% { top: -100px; }
  100% { top: 100vh; }
}

.glitch-header h1 {
  font-size: 3rem;
  color: var(--neon-cyan);
  text-shadow: 0 0 10px var(--neon-cyan);
  text-transform: uppercase;
  letter-spacing: 4px;
}

.subtitle {
  color: var(--neon-purple);
  font-size: 1.2rem;
  margin-top: -10px;
}

.neon-btn {
  display: inline-block;
  padding: 10px 20px;
  border: 1px solid var(--neon-cyan);
  color: var(--neon-cyan);
  text-decoration: none;
  background: transparent;
  transition: all 0.3s ease;
  box-shadow: 0 0 5px var(--neon-cyan) inset;
}

.neon-btn:hover {
  background: var(--neon-cyan);
  color: var(--dark-bg);
  box-shadow: 0 0 20px var(--neon-cyan);
}

.cyber-footer {
  text-align: center;
  margin-top: 4rem;
  padding-top: 2rem;
  border-top: 1px solid var(--neon-purple);
}
</style>