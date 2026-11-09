<template>
  <section class="section-container">
    <div class="section-header">
      <h2 class="section-title">Technical Skills</h2>
      <p class="section-description">Core programming languages, application frameworks, and system tools.</p>
    </div>

    <div class="skills-grid">
      <!-- Languages -->
      <div class="skill-category-card">
        <div class="category-header">
          <svg class="category-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <polyline points="16 18 22 12 16 6"/>
            <polyline points="8 6 2 12 8 18"/>
          </svg>
          <h3 class="category-title">Languages</h3>
        </div>
        <div class="tag-cloud">
          <span class="skill-tag">JavaScript</span>
          <span class="skill-tag">Java</span>
          <span class="skill-tag">C++</span>
          <span class="skill-tag">Swift</span>
          <span class="skill-tag">SQL</span>
        </div>
      </div>

      <!-- Frontend Architecture -->
      <div class="skill-category-card">
        <div class="category-header">
          <svg class="category-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <rect width="18" height="18" x="3" y="3" rx="2"/>
            <path d="M3 9h18M9 21V9"/>
          </svg>
          <h3 class="category-title">Frontend Architecture</h3>
        </div>
        <div class="tag-cloud">
          <span class="skill-tag">Vue.js</span>
          <span class="skill-tag">React.js</span>
          <span class="skill-tag">Pinia</span>
          <span class="skill-tag">SwiftUI / UIKit</span>
          <span class="skill-tag">Tailwind CSS</span>
        </div>
      </div>

      <!-- Backend & Databases -->
      <div class="skill-category-card">
        <div class="category-header">
          <svg class="category-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <ellipse cx="12" cy="5" rx="9" ry="3"/>
            <path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/>
            <path d="M3 12c0 1.66 4 3 9 3s9-1.34 9-3"/>
          </svg>
          <h3 class="category-title">Backend & Systems</h3>
        </div>
        <div class="tag-cloud">
          <span class="skill-tag">Spring Boot</span>
          <span class="skill-tag">Node.js</span>
          <span class="skill-tag">Express.js</span>
          <span class="skill-tag">MongoDB</span>
          <span class="skill-tag">System Design</span>
        </div>
      </div>

      <!-- Testing & Tools -->
      <div class="skill-category-card">
        <div class="category-header">
          <svg class="category-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"/>
          </svg>
          <h3 class="category-title">Testing & DevOps</h3>
        </div>
        <div class="tag-cloud">
          <span class="skill-tag">Cypress</span>
          <span class="skill-tag">Jest</span>
          <span class="skill-tag">Mocha</span>
          <span class="skill-tag">Postman</span>
          <span class="skill-tag">Git / CI Pipelines</span>
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

.skills-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.skill-category-card {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-lg);
  padding: 20px 24px;
  transition: border-color 140ms var(--ease-standard);
}

.skill-category-card:hover {
  border-color: var(--border-hover);
}

.category-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 16px;
  padding-bottom: 12px;
  border-bottom: 1px solid var(--border-hairline);
}

.category-icon {
  width: 16px;
  height: 16px;
  color: var(--accent);
  flex-shrink: 0;
}

.category-title {
  margin: 0;
  font-size: 14px;
  font-weight: 600;
  color: var(--text-primary);
  letter-spacing: -0.01em;
}

.tag-cloud {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-tag {
  font-size: 12px;
  font-family: var(--font-mono);
  color: var(--text-secondary);
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  padding: 4px 10px;
  border-radius: var(--radius-sm);
  transition: all 120ms var(--ease-standard);
}

.skill-tag:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
}

@media (max-width: 640px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>
