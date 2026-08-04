<template>
  <section class="cyber-panel contact-panel">
    <div class="panel-header">
      <h2>// TRANSMISSION_PROTOCOLS: CONTACT</h2>
    </div>
    
    <div class="contact-container">
      <p class="terminal-text">> SECURE CONNECTION ESTABLISHED. SELECT A CHANNEL TO INITIATE COMM_LINK:</p>
      
      <div class="action-grid">
        <!-- Email -->
        <a href="mailto:shivamdubey177@gmail.com" class="cyber-btn email-btn">
          <span class="btn-icon">✉</span>
          <span class="btn-text">INITIALIZE_EMAIL</span>
          <span class="btn-glitch"></span>
        </a>

        <!-- LinkedIn -->
        <a href="https://linkedin.com/in/shivam-dubey-aa47571ba" target="_blank" rel="noopener noreferrer" class="cyber-btn linkedin-btn">
          <span class="btn-icon">in</span>
          <span class="btn-text">LINKEDIN_UPLINK</span>
          <span class="btn-glitch"></span>
        </a>

        <!-- GitHub -->
        <a href="https://github.com/ICHIGO606" target="_blank" rel="noopener noreferrer" class="cyber-btn github-btn">
          <span class="btn-icon">&lt;/&gt;</span>
          <span class="btn-text">GITHUB_DATABANK</span>
          <span class="btn-glitch"></span>
        </a>
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
  position: relative;
}

/* Background warning stripes effect */
.contact-panel::before {
  content: '';
  position: absolute;
  top: 0; right: 0; bottom: 0; width: 100%;
  background: repeating-linear-gradient(
    45deg,
    transparent,
    transparent 10px,
    rgba(176, 38, 255, 0.03) 10px,
    rgba(176, 38, 255, 0.03) 20px
  );
  pointer-events: none;
  z-index: 0;
}

.panel-header h2 {
  color: var(--neon-cyan);
  margin-top: 0;
  border-bottom: 1px solid #333;
  padding-bottom: 0.8rem;
  margin-bottom: 1.5rem;
  position: relative;
  z-index: 1;
}

.contact-container {
  position: relative;
  z-index: 1;
}

.terminal-text {
  font-family: 'Courier New', Courier, monospace;
  color: #aaa;
  margin-bottom: 2rem;
  font-size: 0.95rem;
}

.action-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

/* Cybernetic Button Base */
.cyber-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  background: rgba(0, 0, 0, 0.6);
  border: 1px solid #444;
  padding: 1rem;
  color: #fff;
  text-decoration: none;
  font-family: 'Courier New', Courier, monospace;
  font-weight: bold;
  letter-spacing: 1px;
  position: relative;
  overflow: hidden;
  transition: all 0.3s ease;
  clip-path: polygon(10% 0, 100% 0, 100% 70%, 90% 100%, 0 100%, 0 30%);
}

.btn-icon {
  font-size: 1.2rem;
  font-weight: normal;
}

/* Hover Effects */
.cyber-btn:hover {
  background: rgba(0, 0, 0, 0.8);
  transform: translateY(-3px);
}

.email-btn:hover {
  border-color: var(--neon-cyan);
  color: var(--neon-cyan);
  box-shadow: 0 0 15px rgba(0, 240, 255, 0.3) inset;
}

.linkedin-btn:hover {
  border-color: #0077b5; /* LinkedIn Blue */
  color: #0077b5;
  box-shadow: 0 0 15px rgba(0, 119, 181, 0.3) inset;
}

.github-btn:hover {
  border-color: var(--neon-purple);
  color: var(--neon-purple);
  box-shadow: 0 0 15px rgba(176, 38, 255, 0.3) inset;
}

/* Hover Glitch Line Animation */
.btn-glitch {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 2px;
  background: #fff;
  transition: all 0.3s ease;
}

.email-btn .btn-glitch { background: var(--neon-cyan); }
.linkedin-btn .btn-glitch { background: #0077b5; }
.github-btn .btn-glitch { background: var(--neon-purple); }

.cyber-btn:hover .btn-glitch {
  animation: scanline 0.8s linear infinite;
}

@keyframes scanline {
  0% { top: 0; left: -100%; }
  50% { top: 50%; left: 0; }
  100% { top: 100%; left: 100%; }
}
</style>