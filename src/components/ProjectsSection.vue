<template>
  <section class="cyber-panel database-panel">
    <div class="panel-header">
      <h2>// DATABANKS: PROJECTS</h2>
    </div>
    
    <div class="projects-grid">
      <!-- Fight Hub (MMA) -->
      <div class="project-card holo-card">
        <div class="card-header">
          <span class="sys-icon">▣</span>
          <span class="status-indicator active">SYS.ACTIVE</span>
        </div>
        <h3>Fight Hub (MMA Stats)</h3>
        <div class="tech-tags">
          <span>Vue.js</span>
          <span>Spring Boot</span>
          <span>APIs</span>
          <span>Interactive Data</span>
        </div>
        <div class="card-divider"></div>
        <p class="description">
          A statistical dashboard and hub tracking real-time metrics and data for MMA events, featuring dynamic visualizations and a modern frontend interface.
        </p>
      </div>

      <!-- Attire Me -->
      <div class="project-card holo-card">
        <div class="card-header">
          <span class="sys-icon">▣</span>
          <span class="status-indicator">SYS.ARCHIVED</span>
        </div>
        <h3>Attire Me Outfit Recommender</h3>
        <div class="tech-tags">
          <span>Swift</span>
          <span>Supabase</span>
          <span>Cloudinary</span>
          <span>iOS</span>
        </div>
        <div class="card-divider"></div>
        <p class="description">
          Developed an iOS app recommending outfits based on preferences and weather, driving a 30% engagement increase. Built a community feature increasing user retention by 50%.
        </p>
      </div>

      <!-- Blinkit Clone -->
      <div class="project-card holo-card">
        <div class="card-header">
          <span class="sys-icon">▣</span>
          <span class="status-indicator">SYS.ARCHIVED</span>
        </div>
        <h3>BringIt Blinkit Clone</h3>
        <div class="tech-tags">
          <span>React.js</span>
          <span>Node.js</span>
          <span>Express.js</span>
          <span>MongoDB</span>
        </div>
        <div class="card-divider"></div>
        <p class="description">
          Built a full-stack grocery delivery application with JWT authentication, reducing unauthorized access by 80%. Designed dynamic product listings and efficient backend API endpoints.
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.cyber-panel {
  background: var(--panel-bg);
  border-left: 4px solid var(--neon-cyan);
  padding: 1.5rem;
  margin: 2rem 0;
  box-shadow: 0 0 15px rgba(0, 240, 255, 0.05);
}

.panel-header h2 {
  color: var(--neon-purple);
  margin-top: 0;
  border-bottom: 1px solid #333;
  padding-bottom: 0.8rem;
  margin-bottom: 2rem;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2rem;
}

/* Holographic Card Effect */
.holo-card {
  position: relative;
  background: rgba(10, 10, 15, 0.8);
  border: 1px solid rgba(0, 240, 255, 0.2);
  padding: 1.5rem;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  overflow: hidden;
}

/* Corner Targeting Brackets */
.holo-card::before, .holo-card::after {
  content: '';
  position: absolute;
  width: 20px;
  height: 20px;
  border: 2px solid transparent;
  transition: all 0.3s ease;
}

.holo-card::before {
  top: 0;
  left: 0;
  border-top-color: rgba(0, 240, 255, 0.5);
  border-left-color: rgba(0, 240, 255, 0.5);
}

.holo-card::after {
  bottom: 0;
  right: 0;
  border-bottom-color: rgba(0, 240, 255, 0.5);
  border-right-color: rgba(0, 240, 255, 0.5);
}

.holo-card:hover {
  border-color: var(--neon-cyan);
  box-shadow: 0 5px 20px rgba(0, 240, 255, 0.15), 0 0 10px rgba(0, 240, 255, 0.1) inset;
  transform: translateY(-5px);
}

.holo-card:hover::before, .holo-card:hover::after {
  width: 100%;
  height: 100%;
  border-color: var(--neon-cyan);
  opacity: 0.1;
}

/* Card Internals */
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  font-family: 'Courier New', Courier, monospace;
  font-size: 0.85rem;
}

.sys-icon {
  color: var(--neon-purple);
  font-size: 1.2rem;
}

.status-indicator {
  color: #666;
  border: 1px solid #444;
  padding: 2px 6px;
  background: rgba(0,0,0,0.5);
}

.status-indicator.active {
  color: var(--neon-cyan);
  border-color: var(--neon-cyan);
  text-shadow: 0 0 5px var(--neon-cyan);
}

.holo-card h3 {
  margin: 0 0 1rem 0;
  color: #fff;
  font-size: 1.2rem;
  letter-spacing: 0.5px;
}

/* Tech Tags / Pills */
.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.2rem;
}

.tech-tags span {
  background: rgba(176, 38, 255, 0.1);
  color: var(--neon-purple);
  border: 1px solid rgba(176, 38, 255, 0.3);
  padding: 4px 10px;
  font-size: 0.8rem;
  border-radius: 2px;
}

.card-divider {
  height: 1px;
  background: linear-gradient(90deg, rgba(0, 240, 255, 0.3), transparent);
  margin-bottom: 1rem;
}

.description {
  color: #bbb;
  font-size: 0.95rem;
  line-height: 1.5;
  margin: 0;
}
</style>