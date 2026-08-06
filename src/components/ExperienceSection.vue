<template>
  <section class="cyber-panel timeline-panel">
    <div class="panel-header">
      <h2>// EXECUTION_LOG: EXPERIENCE</h2>
    </div>
    
    <div class="timeline-container">
      <!-- Lumen Technologies -->
      <div class="timeline-item">
        <div class="timeline-marker pulse"></div>
        <div class="job-card glow-hover">
          <div class="job-header">
            <div class="title-group">
              <h3>Lumen Technologies India</h3>
              <span class="role">Frontend Intern</span>
            </div>
            <span class="badge active-badge">Ongoing - Aug 2024</span>
          </div>
          <div class="card-divider"></div>
          <ul class="task-list">
            <li>Engineered frontend interfaces utilizing Vue.js and the organization's proprietary CSS framework.</li>
            <li>Implemented robust software testing pipelines utilizing Cypress, Jest, and Mocha.</li>
            <li>Executed remediation protocols for GitHub security findings, ensuring high code integrity and system security.</li>
          </ul>
        </div>
      </div>

      <!-- Infosys -->
      <div class="timeline-item">
        <div class="timeline-marker"></div>
        <div class="job-card glow-hover">
          <div class="job-header">
            <div class="title-group">
              <h3>Infosys</h3>
              <span class="role">iOS Developer Intern</span>
            </div>
            <span class="badge">Feb 2025</span>
          </div>
          <div class="card-divider"></div>
          <ul class="task-list">
            <li>Collaborated in a 10-member team to build scalable iOS applications using agile methodologies.</li>
            <li>Contributed to building UI components and integrating RESTful APIs in Swift.</li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.cyber-panel {
  background: var(--panel-bg);
  border-left: 4px solid var(--neon-purple);
  padding: 1.5rem;
  margin: 2rem 0;
  box-shadow: 0 0 15px rgba(176, 38, 255, 0.05);
}

.panel-header h2 {
  color: var(--neon-cyan);
  margin-top: 0;
  border-bottom: 1px solid #333;
  padding-bottom: 0.8rem;
  margin-bottom: 2rem;
}

/* Timeline Layout */
.timeline-container {
  position: relative;
  margin-left: 1rem;
  padding-left: 2rem;
  border-left: 2px dashed rgba(0, 240, 255, 0.3);
}

.timeline-item {
  position: relative;
  margin-bottom: 2.5rem;
}

.timeline-item:last-child {
  margin-bottom: 0;
}

/* Glowing Nodes */
.timeline-marker {
  position: absolute;
  left: -2.45rem;
  top: 1.2rem;
  width: 12px;
  height: 12px;
  background-color: var(--dark-bg);
  border: 2px solid var(--neon-cyan);
  border-radius: 50%;
  box-shadow: 0 0 10px var(--neon-cyan);
  z-index: 2;
}

.pulse {
  animation: pulse-glow 2s infinite;
  background-color: var(--neon-cyan);
}

@keyframes pulse-glow {
  0% { box-shadow: 0 0 0 0 rgba(0, 240, 255, 0.7); }
  70% { box-shadow: 0 0 0 10px rgba(0, 240, 255, 0); }
  100% { box-shadow: 0 0 0 0 rgba(0, 240, 255, 0); }
}

/* Job Cards & Hover Effects */
.job-card {
  padding: 1.5rem;
  border: 1px solid rgba(176, 38, 255, 0.3);
  background: rgba(0, 0, 0, 0.6);
  border-radius: 4px;
  position: relative;
  transition: all 0.3s ease;
}

.job-card::before {
  content: '';
  position: absolute;
  top: 1.5rem;
  left: -1rem;
  border-width: 8px 10px 8px 0;
  border-style: solid;
  border-color: transparent rgba(176, 38, 255, 0.3) transparent transparent;
  transition: border-color 0.3s ease;
}

.glow-hover:hover {
  border-color: var(--neon-purple);
  box-shadow: 0 0 20px rgba(176, 38, 255, 0.15) inset, 0 5px 15px rgba(0, 0, 0, 0.5);
  transform: translateX(5px);
}

.glow-hover:hover::before {
  border-color: transparent var(--neon-purple) transparent transparent;
}

/* Typography & Alignment */
.job-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 1rem;
}

.title-group h3 {
  margin: 0 0 0.3rem 0;
  color: #fff;
  font-size: 1.3rem;
  letter-spacing: 1px;
}

.role {
  color: var(--neon-purple);
  font-size: 0.95rem;
  font-weight: bold;
}

.badge {
  background: rgba(0, 240, 255, 0.05);
  color: #aaa;
  padding: 5px 10px;
  border: 1px solid #444;
  font-size: 0.85rem;
  font-family: 'Courier New', Courier, monospace;
}

.active-badge {
  color: var(--neon-cyan);
  border-color: var(--neon-cyan);
  box-shadow: 0 0 8px rgba(0, 240, 255, 0.2);
}

.card-divider {
  height: 1px;
  background: linear-gradient(90deg, rgba(176, 38, 255, 0.5), transparent);
  margin: 1.2rem 0;
}

.task-list {
  margin: 0;
  padding-left: 1.2rem;
  color: #ccc;
  line-height: 1.6;
}

.task-list li {
  margin-bottom: 0.8rem;
}

.task-list li::marker {
  color: var(--neon-cyan);
  content: "» ";
}
</style>