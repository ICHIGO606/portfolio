<template>
  <button 
    type="button" 
    class="theme-toggle-btn"
    @click="toggleTheme" 
    :aria-label="theme === 'dark' ? 'Switch to light theme' : 'Switch to dark theme'"
    :title="theme === 'dark' ? 'Switch to light theme' : 'Switch to dark theme'"
  >
    <!-- Sun icon (shown in dark mode) -->
    <svg v-if="theme === 'dark'" class="theme-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
      <circle cx="12" cy="12" r="4"/>
      <path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M6.34 17.66l-1.41 1.41M19.07 4.93l-1.41 1.41"/>
    </svg>
    <!-- Moon icon (shown in light mode) -->
    <svg v-else class="theme-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
      <path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"/>
    </svg>
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const theme = ref('dark')

const applyTheme = (newTheme) => {
  theme.value = newTheme
  document.documentElement.setAttribute('data-theme', newTheme)
  localStorage.setItem('shivam_theme', newTheme)
}

const toggleTheme = () => {
  applyTheme(theme.value === 'dark' ? 'light' : 'dark')
}

onMounted(() => {
  const saved = localStorage.getItem('shivam_theme')
  if (saved) {
    applyTheme(saved)
  } else if (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches) {
    applyTheme('light')
  } else {
    applyTheme('dark')
  }
})

defineExpose({
  theme,
  toggleTheme
})
</script>

<style scoped>
.theme-toggle-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  color: var(--text-secondary);
  cursor: pointer;
  transition: all 140ms var(--ease-standard);
  padding: 0;
}

.theme-toggle-btn:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
  background-color: var(--bg-surface);
}

.theme-icon {
  width: 16px;
  height: 16px;
}
</style>

