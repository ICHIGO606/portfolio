<template>
  <section class="section-container">
    <div class="section-header">
      <h2 class="section-title">Contact</h2>
      <p class="section-description">Available for software engineering roles, discussions on systems design, or open-source collaboration.</p>
    </div>

    <div class="contact-card">
      <div class="card-message">
        <h3 class="message-title">Let’s connect</h3>
        <p class="message-text">
          Whether you have an opening for a software engineer, questions about my projects, or want to discuss frontend architecture, feel free to drop an email or reach out on social channels.
        </p>
      </div>

      <div class="contact-channels">
        <!-- Email with Copy Action -->
        <div class="channel-btn primary-channel email-card">
          <a href="mailto:shivamdubey177@gmail.com" class="channel-link">
            <svg class="channel-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect width="20" height="16" x="2" y="4" rx="2"/>
              <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
            </svg>
            <div class="channel-info">
              <span class="channel-label">Email</span>
              <span class="channel-value">shivamdubey177@gmail.com</span>
            </div>
          </a>
          <button 
            type="button" 
            class="copy-btn" 
            :class="{ copied }"
            @click="copyEmail" 
            :aria-label="copied ? 'Email copied' : 'Copy email to clipboard'"
          >
            <svg v-if="!copied" class="copy-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect width="14" height="14" x="8" y="8" rx="2" ry="2"/>
              <path d="M4 16c-1.1 0-2-.9-2-2V4c0-1.1.9-2 2-2h10c1.1 0 2 .9 2 2"/>
            </svg>
            <svg v-else class="copy-icon check-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <polyline points="20 6 9 17 4 12"/>
            </svg>
            <span>{{ copied ? 'Copied' : 'Copy' }}</span>
          </button>
        </div>

        <!-- LinkedIn -->
        <a href="https://linkedin.com/in/shivam-dubey-aa47571ba" target="_blank" rel="noopener noreferrer" class="channel-btn">
          <svg class="channel-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
            <rect width="4" height="12" x="2" y="9"/>
            <circle cx="4" cy="4" r="2"/>
          </svg>
          <div class="channel-info">
            <span class="channel-label">LinkedIn</span>
            <span class="channel-value">shivam-dubey-aa47571ba</span>
          </div>
        </a>

        <!-- GitHub -->
        <a href="https://github.com/ICHIGO606" target="_blank" rel="noopener noreferrer" class="channel-btn">
          <svg class="channel-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/>
            <path d="M9 18c-4.51 2-5-2-7-2"/>
          </svg>
          <div class="channel-info">
            <span class="channel-label">GitHub</span>
            <span class="channel-value">github.com/ICHIGO606</span>
          </div>
        </a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const copied = ref(false)

const copyEmail = async () => {
  try {
    await navigator.clipboard.writeText('shivamdubey177@gmail.com')
    copied.value = true
    setTimeout(() => {
      copied.value = false
    }, 2000)
  } catch (err) {
    console.error('Failed to copy', err)
  }
}
</script>

<style scoped>
.section-container {
  margin-bottom: 24px;
}

.section-header {
  margin-bottom: 28px;
}

.section-title {
  margin: 0 0 6px;
  font-size: 20px;
  font-weight: 600;
  letter-spacing: -0.015em;
  color: var(--text-primary);
}

.section-description {
  margin: 0;
  font-size: 13px;
  color: var(--text-muted);
}

.contact-card {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-xl);
  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.card-message {
  max-width: 680px;
}

.message-title {
  margin: 0 0 8px;
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
}

.message-text {
  margin: 0;
  font-size: 14px;
  line-height: 1.6;
  color: var(--text-secondary);
}

.contact-channels {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 14px;
}

.channel-btn {
  display: flex;
  align-items: center;
  gap: 14px;
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  padding: 14px 18px;
  transition: all 140ms var(--ease-standard);
}

.channel-btn:hover {
  border-color: var(--border-hover);
  background-color: var(--bg-surface-hover);
  transform: translateY(-1px);
}

.primary-channel {
  border-color: var(--accent-border);
  background-color: var(--accent-muted);
}

.primary-channel:hover {
  border-color: var(--accent);
  background-color: rgba(56, 189, 248, 0.15);
}

.primary-channel .channel-icon {
  color: var(--accent);
}

.channel-icon {
  width: 18px;
  height: 18px;
  color: var(--text-secondary);
  flex-shrink: 0;
}

.channel-info {
  display: flex;
  flex-direction: column;
  gap: 2px;
  min-width: 0;
}

.channel-label {
  font-size: 11px;
  font-weight: 500;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.channel-value {
  font-size: 13px;
  font-family: var(--font-mono);
  color: var(--text-primary);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.email-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 14px 10px 18px;
}

.channel-link {
  display: flex;
  align-items: center;
  gap: 14px;
  flex: 1;
  min-width: 0;
  text-decoration: none;
  color: inherit;
}

.copy-btn {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  color: var(--text-secondary);
  font-size: 11px;
  font-family: var(--font-mono);
  padding: 5px 8px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all 120ms var(--ease-standard);
  flex-shrink: 0;
}

.copy-btn:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
}

.copy-btn.copied {
  color: var(--success);
  border-color: rgba(76, 195, 138, 0.4);
  background-color: rgba(76, 195, 138, 0.08);
}

.copy-icon {
  width: 13px;
  height: 13px;
}

.check-icon {
  color: var(--success);
}
</style>
