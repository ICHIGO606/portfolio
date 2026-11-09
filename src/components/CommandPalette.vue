<template>
  <div v-if="isOpen" class="cmd-overlay" @click.self="close">
    <div class="cmd-dialog" role="dialog" aria-modal="true" aria-label="Command Menu">
      <div class="cmd-search-bar">
        <svg class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <circle cx="11" cy="11" r="8"/>
          <path d="m21 21-4.3-4.3"/>
        </svg>
        <input 
          ref="inputRef"
          v-model="query" 
          type="text" 
          class="cmd-input"
          placeholder="Search actions, projects, or jump to section..."
          @keydown.down.prevent="navigateDown"
          @keydown.up.prevent="navigateUp"
          @keydown.enter.prevent="selectActive"
          @keydown.esc="close"
        />
        <kbd class="esc-kbd" @click="close">ESC</kbd>
      </div>

      <div class="cmd-list" ref="listRef">
        <div v-if="filteredItems.length === 0" class="cmd-empty">
          No matching commands found.
        </div>

        <template v-else>
          <div 
            v-for="(item, index) in filteredItems" 
            :key="item.id"
            :class="['cmd-item', { active: activeIndex === index }]"
            @mouseenter="activeIndex = index"
            @click="execute(item)"
          >
            <div class="item-left">
              <span class="item-icon-box">
                <svg v-if="item.category === 'Navigation'" class="item-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="m9 18 6-6-6-6"/>
                </svg>
                <svg v-else-if="item.category === 'Architecture'" class="item-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M12 2 2 7l10 5 10-5-10-5Z"/>
                  <path d="m2 17 10 5 10-5"/>
                  <path d="m2 12 10 5 10-5"/>
                </svg>
                <svg v-else-if="item.id === 'theme'" class="item-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <circle cx="12" cy="12" r="4"/>
                  <path d="M12 2v2M12 20v2M4.93 4.93l1.41 1.41M17.66 17.66l1.41 1.41M2 12h2M20 12h2M6.34 17.66l-1.41 1.41M19.07 4.93l-1.41 1.41"/>
                </svg>
                <svg v-else-if="item.id === 'copy-email'" class="item-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <rect width="14" height="14" x="8" y="8" rx="2" ry="2"/>
                  <path d="M4 16c-1.1 0-2-.9-2-2V4c0-1.1.9-2 2-2h10c1.1 0 2 .9 2 2"/>
                </svg>
                <svg v-else class="item-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/>
                  <polyline points="15 3 21 3 21 9"/>
                  <line x1="10" y1="14" x2="21" y2="3"/>
                </svg>
              </span>
              <div class="item-titles">
                <span class="item-title">{{ item.title }}</span>
                <span v-if="item.subtitle" class="item-subtitle">{{ item.subtitle }}</span>
              </div>
            </div>

            <span class="item-badge">{{ item.category }}</span>
          </div>
        </template>
      </div>

      <div class="cmd-footer">
        <span class="hint">Use <kbd>↑</kbd> <kbd>↓</kbd> to navigate</span>
        <span class="hint"><kbd>↵</kbd> to select</span>
        <span class="hint"><kbd>esc</kbd> to dismiss</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch, nextTick, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  isOpen: Boolean
})

const emit = defineEmits(['update:isOpen', 'toggle-theme', 'open-architecture', 'copy-email'])

const query = ref('')
const activeIndex = ref(0)
const inputRef = ref(null)
const listRef = ref(null)

const items = [
  // Navigation
  { id: 'about', title: 'About Shivam Dubey', subtitle: 'Academic background & engineering overview', category: 'Navigation', action: () => scrollTo('#about') },
  { id: 'experience', title: 'Work Experience', subtitle: 'Frontend Intern at Lumen & iOS Intern at Infosys', category: 'Navigation', action: () => scrollTo('#experience') },
  { id: 'projects', title: 'Featured Projects', subtitle: 'Fight Hub, Smart Stay, Attire Me, BringIt', category: 'Navigation', action: () => scrollTo('#projects') },
  { id: 'skills', title: 'Technical Skills Matrix', subtitle: 'Languages, architecture, frameworks & databases', category: 'Navigation', action: () => scrollTo('#skills') },
  { id: 'contact', title: 'Contact & Channels', subtitle: 'Email, GitHub, LinkedIn links', category: 'Navigation', action: () => scrollTo('#contact') },

  // Architecture Specs
  { id: 'arch-fight-hub', title: 'Fight Hub Architecture', subtitle: 'Spring Boot reactive ingestion & striking metrics engine', category: 'Architecture', action: () => emit('open-architecture', 'fight-hub') },
  { id: 'arch-smart-stay', title: 'Smart Stay Architecture', subtitle: 'State machine, concurrency locks & PostgreSQL schema', category: 'Architecture', action: () => emit('open-architecture', 'smart-stay') },
  { id: 'arch-attire-me', title: 'Attire Me Architecture', subtitle: 'iOS MVVM, offline caching & WeatherAPI mapper', category: 'Architecture', action: () => emit('open-architecture', 'attire-me') },
  { id: 'arch-bring-it', title: 'BringIt Architecture', subtitle: 'JWT rotation & atomic MongoDB inventory operations', category: 'Architecture', action: () => emit('open-architecture', 'bring-it') },

  // Quick Actions
  { id: 'copy-email', title: 'Copy Email Address', subtitle: 'shivamdubey177@gmail.com', category: 'Action', action: () => emit('copy-email') },
  { id: 'theme', title: 'Toggle Light / Dark Mode', subtitle: 'Switch between Ink Dark & Daylight Light', category: 'Action', action: () => emit('toggle-theme') },

  // Socials
  { id: 'github', title: 'Open GitHub Profile', subtitle: 'github.com/ICHIGO606', category: 'External', action: () => window.open('https://github.com/ICHIGO606', '_blank') },
  { id: 'linkedin', title: 'Open LinkedIn Profile', subtitle: 'linkedin.com/in/shivam-dubey-aa47571ba', category: 'External', action: () => window.open('https://linkedin.com/in/shivam-dubey-aa47571ba', '_blank') },
]

const filteredItems = computed(() => {
  if (!query.value.trim()) return items
  const q = query.value.toLowerCase()
  return items.filter(item => 
    item.title.toLowerCase().includes(q) ||
    item.subtitle?.toLowerCase().includes(q) ||
    item.category.toLowerCase().includes(q)
  )
})

watch(filteredItems, () => {
  activeIndex.value = 0
})

watch(() => props.isOpen, (newVal) => {
  if (newVal) {
    query.value = ''
    activeIndex.value = 0
    nextTick(() => {
      inputRef.value?.focus()
    })
  }
})

const close = () => {
  emit('update:isOpen', false)
}

const navigateDown = () => {
  if (filteredItems.value.length === 0) return
  activeIndex.value = (activeIndex.value + 1) % filteredItems.value.length
}

const navigateUp = () => {
  if (filteredItems.value.length === 0) return
  activeIndex.value = (activeIndex.value - 1 + filteredItems.value.length) % filteredItems.value.length
}

const selectActive = () => {
  const item = filteredItems.value[activeIndex.value]
  if (item) execute(item)
}

const execute = (item) => {
  close()
  item.action?.()
}

const scrollTo = (hash) => {
  const el = document.querySelector(hash)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}

// Global keyboard shortcut
const handleKeyDown = (e) => {
  if ((e.metaKey || e.ctrlKey) && e.key.toLowerCase() === 'k') {
    e.preventDefault()
    emit('update:isOpen', !props.isOpen)
  }
  if (e.key === 'Escape' && props.isOpen) {
    close()
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeyDown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeyDown)
})
</script>

<style scoped>
.cmd-overlay {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.65);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  z-index: 999;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding: 80px 16px 24px;
}

.cmd-dialog {
  width: 100%;
  max-width: 580px;
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-xl);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.cmd-search-bar {
  display: flex;
  align-items: center;
  padding: 14px 18px;
  border-bottom: 1px solid var(--border-hairline);
  gap: 12px;
}

.search-icon {
  width: 18px;
  height: 18px;
  color: var(--text-muted);
  flex-shrink: 0;
}

.cmd-input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  font-family: var(--font-sans);
  font-size: 14px;
  color: var(--text-primary);
}

.cmd-input::placeholder {
  color: var(--text-muted);
}

.esc-kbd {
  font-size: 11px;
  font-family: var(--font-mono);
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: 4px;
  padding: 2px 6px;
  color: var(--text-muted);
  cursor: pointer;
}

.cmd-list {
  max-height: 340px;
  overflow-y: auto;
  padding: 8px;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.cmd-empty {
  padding: 24px;
  text-align: center;
  font-size: 13px;
  color: var(--text-muted);
}

.cmd-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 12px;
  border-radius: var(--radius-md);
  cursor: pointer;
  transition: all 100ms var(--ease-standard);
}

.cmd-item.active {
  background-color: var(--bg-surface-raised);
}

.item-left {
  display: flex;
  align-items: center;
  gap: 12px;
  min-width: 0;
}

.item-icon-box {
  width: 24px;
  height: 24px;
  border-radius: 6px;
  background-color: var(--bg-surface-raised);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: var(--text-secondary);
}

.cmd-item.active .item-icon-box {
  color: var(--accent);
}

.item-icon {
  width: 14px;
  height: 14px;
}

.item-titles {
  display: flex;
  flex-direction: column;
  gap: 2px;
  min-width: 0;
}

.item-title {
  font-size: 13px;
  font-weight: 500;
  color: var(--text-primary);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.item-subtitle {
  font-size: 11px;
  color: var(--text-muted);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.item-badge {
  font-size: 10px;
  font-family: var(--font-mono);
  color: var(--text-muted);
  background-color: var(--bg-surface-raised);
  padding: 2px 6px;
  border-radius: 4px;
  flex-shrink: 0;
}

.cmd-footer {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 10px 18px;
  background-color: var(--bg-surface-raised);
  border-top: 1px solid var(--border-hairline);
  font-size: 11px;
  color: var(--text-muted);
  font-family: var(--font-mono);
}

.hint kbd {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: 3px;
  padding: 1px 4px;
  font-size: 10px;
}

@media (max-width: 640px) {
  .cmd-overlay {
    padding: 24px 12px;
  }
  .cmd-footer {
    display: none;
  }
}
</style>

