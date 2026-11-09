<template>
  <section class="hero-section">
    <div class="hero-grid">
      <!-- Left Column: Introduction & Primary Meta -->
      <div class="intro-column">
        <div class="status-pill">
          <span class="status-dot"></span>
          <span class="status-text">Available for software engineering roles</span>
        </div>

        <h1 class="hero-title">Shivam Dubey</h1>
        <p class="hero-subtitle">
          Software engineer specializing in frontend architecture, distributed backend services, and high-performance interactive interfaces.
        </p>

        <div class="meta-list">
          <div class="meta-item">
            <svg class="meta-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/>
              <circle cx="12" cy="10" r="3"/>
            </svg>
            <span>India</span>
          </div>

          <div class="meta-item">
            <svg class="meta-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M22 10v6M2 10l10-5 10 5-10 5z"/>
              <path d="M6 12v5c3 3 9 3 12 0v-5"/>
            </svg>
            <span>B.E. Computer Science, Chitkara University</span>
          </div>

          <div class="meta-item">
            <svg class="meta-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <circle cx="12" cy="8" r="6"/>
              <path d="M15.477 12.89 17 22l-5-3-5 3 1.523-9.11"/>
            </svg>
            <span>Academic Performance: <strong class="cgpa-figure">9.09</strong> / 10 CGPA</span>
          </div>
        </div>

        <div class="hero-actions">
          <a href="mailto:shivamdubey177@gmail.com" class="action-btn primary-btn">
            <svg class="btn-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect width="20" height="16" x="2" y="4" rx="2"/>
              <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/>
            </svg>
            <span>Get in touch</span>
          </a>

          <a href="https://github.com/ICHIGO606" target="_blank" rel="noopener noreferrer" class="action-btn secondary-btn" aria-label="GitHub Profile">
            <svg class="btn-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/>
              <path d="M9 18c-4.51 2-5-2-7-2"/>
            </svg>
            <span>GitHub</span>
          </a>

          <a href="https://linkedin.com/in/shivam-dubey-aa47571ba" target="_blank" rel="noopener noreferrer" class="action-btn secondary-btn" aria-label="LinkedIn Profile">
            <svg class="btn-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/>
              <rect width="4" height="12" x="2" y="9"/>
              <circle cx="4" cy="4" r="2"/>
            </svg>
            <span>LinkedIn</span>
          </a>
        </div>
      </div>

      <!-- Right Column: Engineering Snapshot Card -->
      <div class="snapshot-column">
        <div class="snapshot-card">
          <div class="card-header">
            <span class="card-title">Engineering Focus</span>
            <span class="card-tag">Core Competencies</span>
          </div>

          <div class="snapshot-items">
            <div class="snapshot-item">
              <div class="item-meta">
                <span class="item-name">Frontend Architecture</span>
                <span class="item-badge">Vue.js · React · UI/UX</span>
              </div>
              <p class="item-desc">Designing modular component hierarchies, reactive state management (Pinia), and responsive design systems.</p>
            </div>

            <div class="snapshot-item">
              <div class="item-meta">
                <span class="item-name">Backend & Distributed APIs</span>
                <span class="item-badge">Spring Boot · Node.js · Express</span>
              </div>
              <p class="item-desc">Building resilient REST APIs, schema models with SQL/MongoDB, and secure JWT authentication flows.</p>
            </div>

            <div class="snapshot-item">
              <div class="item-meta">
                <span class="item-name">Testing & Quality Assurance</span>
                <span class="item-badge">Cypress · Jest · Mocha</span>
              </div>
              <p class="item-desc">Comprehensive test suites, automated CI pipelines, and remediation of vulnerability findings.</p>
            </div>
          </div>

          <div class="card-footer">
            <span class="footer-note">Actively building production-grade web & iOS applications</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  padding-bottom: 56px;
  border-bottom: 1px solid var(--border-hairline);
  margin-bottom: 56px;
}

.hero-grid {
  display: grid;
  grid-template-columns: 1.15fr 0.85fr;
  gap: 40px;
  align-items: start;
}

/* Status Pill */
.status-pill {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: 9999px;
  padding: 4px 12px;
  margin-bottom: 20px;
}

.status-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background-color: var(--success);
}

.status-text {
  font-size: 12px;
  color: var(--text-secondary);
  font-weight: 500;
}

/* Title & Subtitle */
.hero-title {
  margin: 0 0 12px;
  font-size: 38px;
  font-weight: 600;
  line-height: 1.15;
  letter-spacing: -0.025em;
  color: var(--text-primary);
}

.hero-subtitle {
  margin: 0 0 24px;
  font-size: 16px;
  line-height: 1.6;
  color: var(--text-secondary);
  max-width: 520px;
}

/* Meta list */
.meta-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 32px;
}

.meta-item {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 13px;
  color: var(--text-secondary);
}

.meta-icon {
  width: 16px;
  height: 16px;
  color: var(--text-muted);
  flex-shrink: 0;
}

.cgpa-figure {
  color: var(--text-primary);
  font-family: var(--font-mono);
  font-weight: 500;
}

/* Actions */
.hero-actions {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
}

.action-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  font-weight: 500;
  padding: 10px 18px;
  border-radius: var(--radius-md);
  transition: all 140ms var(--ease-standard);
  cursor: pointer;
}

.primary-btn {
  background-color: var(--btn-primary-bg);
  color: var(--btn-primary-text);
  border: 1px solid transparent;
}

.primary-btn:hover {
  background-color: var(--btn-primary-hover-bg);
  color: var(--btn-primary-hover-text);
  transform: translateY(-1px);
}

.secondary-btn {
  background-color: var(--bg-surface);
  color: var(--text-primary);
  border: 1px solid var(--border-hairline);
}

.secondary-btn:hover {
  background-color: var(--bg-surface-raised);
  border-color: var(--border-hover);
  transform: translateY(-1px);
}

.btn-icon {
  width: 15px;
  height: 15px;
  flex-shrink: 0;
}

/* Snapshot Card */
.snapshot-card {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-lg);
  padding: 20px 24px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
}

.card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-bottom: 14px;
  border-bottom: 1px solid var(--border-hairline);
  margin-bottom: 16px;
}

.card-title {
  font-size: 13px;
  font-weight: 600;
  color: var(--text-primary);
  letter-spacing: -0.01em;
}

.card-tag {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--text-muted);
  background-color: var(--bg-surface-raised);
  padding: 2px 8px;
  border-radius: 4px;
}

.snapshot-items {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.snapshot-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.item-meta {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  flex-wrap: wrap;
}

.item-name {
  font-size: 13px;
  font-weight: 500;
  color: var(--text-primary);
}

.item-badge {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--accent);
}

.item-desc {
  margin: 0;
  font-size: 12px;
  color: var(--text-muted);
  line-height: 1.5;
}

.card-footer {
  margin-top: 18px;
  padding-top: 14px;
  border-top: 1px solid var(--border-hairline);
}

.footer-note {
  font-size: 11px;
  color: var(--text-muted);
  font-family: var(--font-mono);
}

@media (max-width: 860px) {
  .hero-grid {
    grid-template-columns: 1fr;
    gap: 32px;
  }
}
</style>
