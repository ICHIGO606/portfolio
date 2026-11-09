<template>
  <div class="portfolio-root">
    <!-- Quiet Header Navigation -->
    <header class="site-header">
      <div class="header-inner">
        <a href="#" class="brand">
          <span class="brand-name">Shivam Dubey</span>
          <span class="brand-role">Software Engineer</span>
        </a>

        <div class="header-controls">
          <!-- Command Palette Trigger Pill -->
          <button 
            type="button" 
            class="cmd-trigger-btn" 
            @click="isCmdOpen = true" 
            title="Open Command Menu (⌘K)"
            aria-label="Open Command Menu (⌘K)"
          >
            <svg class="cmd-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <circle cx="11" cy="11" r="8"/>
              <path d="m21 21-4.3-4.3"/>
            </svg>
            <span class="cmd-text">Search</span>
            <kbd class="cmd-keycap">⌘K</kbd>
          </button>

          <nav class="nav-links">
            <a href="#about" class="nav-link">About</a>
            <a href="#experience" class="nav-link">Experience</a>
            <a href="#projects" class="nav-link">Projects</a>
            <a href="#skills" class="nav-link">Skills</a>
            <a href="#contact" class="nav-btn">Contact</a>
          </nav>

          <!-- Theme Toggle -->
          <ThemeToggle ref="themeToggleRef" />
        </div>
      </div>
    </header>

    <main class="content-container">
      <HeroSection id="about" />
      <ExperienceSection id="experience" />
      <ProjectsSection id="projects" @open-architecture="handleOpenArchitecture" />
      <SkillsSection id="skills" />
      <ContactsSection id="contact" />
    </main>

    <footer class="site-footer">
      <div class="footer-inner">
        <p class="footer-copy">© {{ currentYear }} Shivam Dubey. Built with Vue.js & precision.</p>
        <div class="footer-links">
          <a href="https://github.com/ICHIGO606" target="_blank" rel="noopener noreferrer">GitHub</a>
          <span class="divider">/</span>
          <a href="https://linkedin.com/in/shivam-dubey-aa47571ba" target="_blank" rel="noopener noreferrer">LinkedIn</a>
          <span class="divider">/</span>
          <a href="mailto:shivamdubey177@gmail.com">Email</a>
        </div>
      </div>
    </footer>

    <!-- Global Command Palette -->
    <CommandPalette 
      v-model:isOpen="isCmdOpen"
      @toggle-theme="handleToggleTheme"
      @open-architecture="handleOpenArchitecture"
      @copy-email="handleCopyEmail"
    />

    <!-- Global Architecture Deep-Dive Drawer -->
    <ArchitectureDrawer 
      :project="selectedProject" 
      @close="selectedProject = null" 
    />

    <!-- Quiet Toast Notification -->
    <div v-if="toastMessage" class="toast-notification" role="status" aria-live="polite">
      <svg class="toast-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
        <polyline points="20 6 9 17 4 12"/>
      </svg>
      <span>{{ toastMessage }}</span>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import HeroSection from './components/HeroSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ContactsSection from './components/ContactsSection.vue'
import ThemeToggle from './components/ThemeToggle.vue'
import CommandPalette from './components/CommandPalette.vue'
import ArchitectureDrawer from './components/ArchitectureDrawer.vue'

const currentYear = computed(() => new Date().getFullYear())

const isCmdOpen = ref(false)
const selectedProject = ref(null)
const themeToggleRef = ref(null)
const toastMessage = ref('')

const handleOpenArchitecture = (projectId) => {
  selectedProject.value = projectId
}

const handleToggleTheme = () => {
  themeToggleRef.value?.toggleTheme()
}

const handleCopyEmail = async () => {
  try {
    await navigator.clipboard.writeText('shivamdubey177@gmail.com')
    showToast('Email copied to clipboard (shivamdubey177@gmail.com)')
  } catch (err) {
    showToast('Failed to copy email')
  }
}

const showToast = (msg) => {
  toastMessage.value = msg
  setTimeout(() => {
    toastMessage.value = ''
  }, 2600)
}
</script>

<style>
/* Design Tokens (Ink Dark Ramp) */
:root {
  --bg-page: #0b0d14;
  --bg-surface: #11141c;
  --bg-surface-raised: #181c26;
  --bg-surface-hover: #1e2432;
  --border-hairline: rgba(238, 240, 245, 0.08);
  --border-hover: rgba(238, 240, 245, 0.16);
  --text-primary: #eef0f5;
  --text-secondary: #a3a9b8;
  --text-muted: #7a8296;
  --accent: #38bdf8;
  --accent-muted: rgba(56, 189, 248, 0.1);
  --accent-border: rgba(56, 189, 248, 0.25);
  --success: #4cc38a;

  /* Button Tokens */
  --btn-primary-bg: #eef0f5;
  --btn-primary-text: #0b0d14;
  --btn-primary-hover-bg: #ffffff;
  --btn-primary-hover-text: #000000;

  /* Telemetry Widget Tokens */
  --telemetry-bg: #07090e;
  --telemetry-box: rgba(255, 255, 255, 0.02);
  --telemetry-track: rgba(255, 255, 255, 0.06);
  --telemetry-border: rgba(238, 240, 245, 0.08);
  
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', Menlo, monospace;

  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;

  --ease-standard: cubic-bezier(0.22, 1, 0.36, 1);
}

/* Light Mode Tokens (Daylight Graphite Ramp from Unslop spec) */
[data-theme="light"] {
  --bg-page: #f8fafc;
  --bg-surface: #ffffff;
  --bg-surface-raised: #f1f5f9;
  --bg-surface-hover: #e2e8f0;
  --border-hairline: rgba(15, 23, 42, 0.08);
  --border-hover: rgba(15, 23, 42, 0.18);
  --text-primary: #0f172a;
  --text-secondary: #475569;
  --text-muted: #64748b;
  --accent: #0284c7;
  --accent-muted: rgba(2, 132, 199, 0.08);
  --accent-border: rgba(2, 132, 199, 0.25);
  --success: #16a34a;

  /* Button Tokens */
  --btn-primary-bg: #0f172a;
  --btn-primary-text: #ffffff;
  --btn-primary-hover-bg: #1e293b;
  --btn-primary-hover-text: #ffffff;

  /* Telemetry Widget Tokens */
  --telemetry-bg: #f1f5f9;
  --telemetry-box: #ffffff;
  --telemetry-track: rgba(15, 23, 42, 0.08);
  --telemetry-border: rgba(15, 23, 42, 0.08);
}

*, *::before, *::after {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

section[id] {
  scroll-margin-top: 80px;
}

body {
  margin: 0;
  background-color: var(--bg-page);
  color: var(--text-primary);
  font-family: var(--font-sans);
  font-size: 14px;
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  transition: background-color 180ms var(--ease-standard), color 180ms var(--ease-standard);
}

/* Base Link Reset */
a {
  color: inherit;
  text-decoration: none;
}

/* Root Wrapper */
.portfolio-root {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Quiet Header */
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
  background-color: var(--bg-page);
  border-bottom: 1px solid var(--border-hairline);
  height: 60px;
  transition: background-color 180ms var(--ease-standard);
}

@supports (backdrop-filter: blur(12px)) or (-webkit-backdrop-filter: blur(12px)) {
  .site-header {
    background-color: rgba(11, 13, 20, 0.85);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
  }
  [data-theme="light"] .site-header {
    background-color: rgba(248, 250, 252, 0.85);
  }
}

.header-inner {
  max-width: 1040px;
  margin: 0 auto;
  height: 100%;
  padding: 0 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}

.brand {
  display: flex;
  align-items: baseline;
  gap: 12px;
}

.brand-name {
  font-size: 15px;
  font-weight: 600;
  letter-spacing: -0.01em;
  color: var(--text-primary);
}

.brand-role {
  font-size: 13px;
  color: var(--text-muted);
}

.header-controls {
  display: flex;
  align-items: center;
  gap: 16px;
}

/* Command Menu Trigger Pill */
.cmd-trigger-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  padding: 5px 10px;
  color: var(--text-secondary);
  font-size: 12px;
  cursor: pointer;
  transition: all 120ms var(--ease-standard);
}

.cmd-trigger-btn:hover {
  border-color: var(--border-hover);
  color: var(--text-primary);
}

.cmd-icon {
  width: 14px;
  height: 14px;
  color: var(--text-muted);
}

.cmd-text {
  font-size: 12px;
}

.cmd-keycap {
  font-size: 10px;
  font-family: var(--font-mono);
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  padding: 1px 5px;
  border-radius: 4px;
  color: var(--text-muted);
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 20px;
}

.nav-link {
  font-size: 13px;
  color: var(--text-secondary);
  transition: color 140ms var(--ease-standard);
}

.nav-link:hover {
  color: var(--text-primary);
}

.nav-btn {
  font-size: 13px;
  font-weight: 500;
  color: var(--text-primary);
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  padding: 5px 12px;
  transition: all 140ms var(--ease-standard);
}

.nav-btn:hover {
  border-color: var(--border-hover);
}

/* Main Container */
.content-container {
  max-width: 1040px;
  width: 100%;
  margin: 0 auto;
  padding: 48px 24px 80px;
  flex: 1;
}

/* Footer */
.site-footer {
  border-top: 1px solid var(--border-hairline);
  padding: 32px 24px;
  background-color: var(--bg-page);
}

.footer-inner {
  max-width: 1040px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  flex-wrap: wrap;
}

.footer-copy {
  margin: 0;
  font-size: 13px;
  color: var(--text-muted);
}

.footer-links {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 13px;
  color: var(--text-muted);
}

.footer-links a {
  transition: color 140ms var(--ease-standard);
}

.footer-links a:hover {
  color: var(--text-primary);
}

.divider {
  color: var(--border-hairline);
}

/* Toast */
.toast-notification {
  position: fixed;
  bottom: 24px;
  right: 24px;
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--accent-border);
  color: var(--text-primary);
  font-size: 13px;
  padding: 10px 16px;
  border-radius: var(--radius-md);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
  display: flex;
  align-items: center;
  gap: 10px;
  z-index: 1001;
  animation: toastFade 180ms var(--ease-standard);
}

.toast-icon {
  width: 16px;
  height: 16px;
  color: var(--accent);
  flex-shrink: 0;
}

@keyframes toastFade {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 820px) {
  .brand-role {
    display: none;
  }
  .nav-link {
    display: none;
  }
}

@media (max-width: 480px) {
  .cmd-text {
    display: none;
  }
}
</style>
