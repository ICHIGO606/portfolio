<template>
  <section class="cyber-panel matrix-panel">
    <div class="panel-header">
      <h2>// CAPABILITIES_MATRIX</h2>
    </div>
    
    <div class="skills-container">

      <div class="skill-category data-node">
        <div class="node-header">> SYS.LANGUAGES</div>
        <div class="tags">
          <span>JavaScript</span>
          <span>Java</span>
          <span>C++</span>
          <span>Swift</span>
          <span>SQL</span>
        </div>
      </div>
      

      <div class="skill-category data-node">
        <div class="node-header">> FRONTEND_ARCH</div>
        <div class="tags">
          <span>Vue.js</span>
          <span>React.js</span>
          <span>Pinia</span>
          <span>SwiftUI / UIKit</span>
          <span>Tailwind CSS</span>
        </div>
      </div>

      <!-- Backend & Databases -->
      <div class="skill-category data-node">
        <div class="node-header">> BACKEND_DB</div>
        <div class="tags">
          <span>Node.js</span>
          <span>Express.js</span>
          <span>Spring Boot</span>
          <span>MongoDB</span>
          <span>System Design</span>
        </div>
      </div>

      <div class="skill-category data-node">
        <div class="node-header">> TOOLS_TESTING</div>
        <div class="tags">
          <span>Cypress</span>
          <span>Jest</span>
          <span>Mocha</span>
          <span>Postman</span>
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

.skills-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

/* Data Node Styling */
.data-node {
  background: rgba(0, 0, 0, 0.4);
  border: 1px solid #222;
  padding: 1.5rem;
  position: relative;
  transition: all 0.3s ease;
}

/* Glowing Corner Brackets */
.data-node::before, .data-node::after {
  content: '';
  position: absolute;
  width: 15px;
  height: 15px;
  border: 2px solid transparent;
  transition: border-color 0.3s ease;
}

.data-node::before {
  top: -1px;
  left: -1px;
  border-top-color: var(--neon-purple);
  border-left-color: var(--neon-purple);
}

.data-node::after {
  bottom: -1px;
  right: -1px;
  border-bottom-color: var(--neon-purple);
  border-right-color: var(--neon-purple);
}

.data-node:hover {
  background: rgba(176, 38, 255, 0.05);
  border-color: rgba(176, 38, 255, 0.3);
}

.data-node:hover::before, .data-node:hover::after {
  border-color: var(--neon-cyan);
}

.node-header {
  font-family: 'Courier New', Courier, monospace;
  font-size: 0.95rem;
  color: var(--neon-cyan);
  border-bottom: 1px dashed #444;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
  letter-spacing: 1px;
}

/* Hex-style Tags */
.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
}

.tags span {
  background: transparent;
  border: 1px solid rgba(0, 240, 255, 0.3);
  color: #ddd;
  padding: 5px 12px;
  font-size: 0.85rem;
  position: relative;
  transition: all 0.2s ease;
  cursor: default;
}

.tags span:hover {
  background: rgba(0, 240, 255, 0.1);
  color: #fff;
  border-color: var(--neon-cyan);
  box-shadow: 0 0 10px rgba(0, 240, 255, 0.4);
  transform: translateY(-2px);
}
</style>