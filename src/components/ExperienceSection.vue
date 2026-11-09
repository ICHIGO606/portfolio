<template>
  <section class="section-container">
    <div class="section-header">
      <h2 class="section-title">Experience</h2>
      <p class="section-description">Practical engineering experience building production web and mobile software.</p>
    </div>

    <div class="timeline">
      <!-- Lumen Technologies -->
      <div class="timeline-entry">
        <div class="timeline-track">
          <div class="timeline-dot current-dot"></div>
          <div class="timeline-line"></div>
        </div>

        <div class="experience-card">
          <div class="card-top">
            <div class="role-group">
              <h3 class="role-title">Intern</h3>
              <span class="company-name">Lumen Technologies India</span>
            </div>
            <span class="period-badge current-badge">Feb 2026 – Present</span>
          </div>

          <ul class="duties-list">
            <li>Engineered modern, responsive frontend user interfaces using Vue.js and company-standard design systems.</li>
            <li>Implemented automated testing pipelines using Cypress, Jest, and Mocha to maintain high code reliability.</li>
            <li>Executed remediation workflows for security and dependency audit findings across core frontend repositories.</li>
          </ul>

          <div class="exp-tech-tags">
            <span class="tag">Vue.js</span>
            <span class="tag">Cypress</span>
            <span class="tag">Jest</span>
            <span class="tag">Mocha</span>
            <span class="tag">Design Systems</span>
          </div>
        </div>
      </div>

      <!-- Infosys -->
      <div class="timeline-entry">
        <div class="timeline-track">
          <div class="timeline-dot"></div>
        </div>

        <div class="experience-card">
          <div class="card-top">
            <div class="role-group">
              <h3 class="role-title">iOS Developer Intern</h3>
              <span class="company-name">Infosys</span>
            </div>
            <span class="period-badge">Feb 2025</span>
          </div>

          <ul class="duties-list">
            <li>Collaborated in an agile team of 10 engineers to build modular iOS features and responsive user interfaces.</li>
            <li>Integrated Swift UI components with RESTful backend services, handling JSON data parsing and state updates.</li>
          </ul>

          <div class="exp-tech-tags">
            <span class="tag">Swift</span>
            <span class="tag">iOS</span>
            <span class="tag">RESTful APIs</span>
            <span class="tag">Agile / Scrum</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-container {
  margin-bottom: 56px;
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

/* Timeline Layout */
.timeline {
  display: flex;
  flex-direction: column;
}

.timeline-entry {
  display: flex;
  gap: 20px;
  position: relative;
}

.timeline-track {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 16px;
  flex-shrink: 0;
}

.timeline-dot {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background-color: var(--bg-surface-raised);
  border: 2px solid var(--text-muted);
  margin-top: 20px;
  z-index: 1;
}

.timeline-dot.current-dot {
  border-color: var(--success);
  background-color: var(--success);
}

.timeline-line {
  width: 1px;
  flex: 1;
  background-color: var(--border-hairline);
  margin: 6px 0;
}

/* Experience Card */
.experience-card {
  flex: 1;
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-lg);
  padding: 20px 24px;
  margin-bottom: 20px;
  transition: border-color 140ms var(--ease-standard);
}

.experience-card:hover {
  border-color: var(--border-hover);
}

.card-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 14px;
  flex-wrap: wrap;
}

.role-group {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.role-title {
  margin: 0;
  font-size: 15px;
  font-weight: 600;
  color: var(--text-primary);
  letter-spacing: -0.01em;
}

.company-name {
  font-size: 13px;
  color: var(--text-secondary);
}

.period-badge {
  font-size: 12px;
  font-family: var(--font-mono);
  color: var(--text-muted);
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  padding: 3px 10px;
  border-radius: var(--radius-sm);
  font-variant-numeric: tabular-nums;
  white-space: nowrap;
}

.current-badge {
  color: var(--text-primary);
  border-color: rgba(76, 195, 138, 0.3);
  background-color: rgba(76, 195, 138, 0.08);
}

/* Duties list */
.duties-list {
  margin: 0;
  padding-left: 18px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.duties-list li {
  font-size: 13px;
  color: var(--text-secondary);
  line-height: 1.55;
}

.duties-list li::marker {
  color: var(--text-muted);
}
</style>
