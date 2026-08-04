<template>
  <section class="cyber-panel hero-panel">
    <div class="panel-header">
      <h2>// SYSTEM_IDENTITY</h2>
      <span class="blinking-cursor"></span>
    </div>
    
    <div class="content-grid">
      <div class="info-block">
        <p><span class="label">STATUS:</span> <span class="status-online">Online</span></p>
        <p><span class="label">LOCATION:</span> India</p>
        <p><span class="label">EDUCATION:</span> Bachelor of Engineering in Computer Science, Chitkara University</p>
        <p><span class="label">CGPA:</span> <span class="highlight">9.09/10</span></p>
      </div>
      
      <div class="contact-block">
        <p class="cmd-prompt">> CONTACT PROTOCOLS:</p>
        <ul class="contact-list">
          <li><a href="mailto:shivamdubey177@gmail.com">EMAIL: shivamdubey177@gmail.com</a></li>
          <li><a href="https://github.com/ICHIGO606" target="_blank">GITHUB: github.com/ICHIGO606</a></li>
          <li><a href="https://linkedin.com/in/shivam-dubey-aa47571ba" target="_blank">LINKEDIN: linkedin.com/in/shivam-dubey-aa47571ba</a></li>
        </ul>
      </div>
      
      <!-- Added a decorative terminal block for extra sci-fi flair -->
      <div class="terminal-block">
        <div class="terminal-header">sys_boot.log</div>
        <div class="terminal-body">
          <p>> INITIALIZING V8 ENGINE ARCHITECTURE... <span class="success">OK</span></p>
          <p>> COMPILING JAVA TRAVERSAL ALGORITHMS... <span class="success">OK</span></p>
          <p>> LOADED: HIGH-LEVEL SYSTEM DESIGN PROTOCOLS</p>
          <p class="blinking-line">> AWAITING USER INPUT<span class="blinking-cursor-inline">_</span></p>
        </div>
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
  box-shadow: 0 0 15px rgba(0, 240, 255, 0.1);
  position: relative;
  overflow: hidden;
}

/* Adds a subtle grid background specifically to the panel */
.cyber-panel::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background: linear-gradient(rgba(0, 240, 255, 0.03) 1px, transparent 1px),
              linear-gradient(90deg, rgba(0, 240, 255, 0.03) 1px, transparent 1px);
  background-size: 20px 20px;
  z-index: 0;
  pointer-events: none;
}

.panel-header {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #333;
  padding-bottom: 0.5rem;
  margin-bottom: 1.5rem;
  position: relative;
  z-index: 1;
}

h2 {
  color: var(--neon-purple);
  margin: 0;
  margin-right: 10px;
}

.content-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  position: relative;
  z-index: 1;
}

.label {
  color: var(--neon-cyan);
  font-weight: bold;
}

.status-online {
  color: #0f0;
  text-shadow: 0 0 8px rgba(0, 255, 0, 0.6);
}

.highlight {
  color: var(--neon-purple);
  font-size: 1.1rem;
  font-weight: bold;
  text-shadow: 0 0 8px rgba(176, 38, 255, 0.6);
}

.cmd-prompt {
  color: var(--neon-purple);
  font-weight: bold;
}

.contact-list {
  list-style-type: none;
  padding: 0;
}

.contact-list li {
  margin-bottom: 0.8rem;
}

.contact-list li::before {
  content: "» ";
  color: var(--neon-cyan);
}

.contact-list a {
  color: #fff;
  text-decoration: none;
  transition: color 0.3s ease, text-shadow 0.3s ease;
}

.contact-list a:hover {
  color: var(--neon-cyan);
  text-shadow: 0 0 8px var(--neon-cyan);
}

/* Terminal Block Styling */
.terminal-block {
  grid-column: 1 / -1; 
  background: rgba(0, 0, 0, 0.7);
  border: 1px solid #333;
  border-top: 2px solid var(--neon-cyan);
  border-radius: 4px;
  font-family: 'Courier New', Courier, monospace;
  font-size: 0.9rem;
  margin-top: 1rem;
}

.terminal-header {
  background: #1a1a24;
  padding: 5px 10px;
  color: #888;
  font-size: 0.8rem;
  border-bottom: 1px solid #333;
}

.terminal-body {
  padding: 15px;
  color: #aaa;
}

.terminal-body p {
  margin: 6px 0;
}

.success {
  color: #0f0;
}

/* Blinking Cursor Animations */
.blinking-cursor {
  display: inline-block;
  width: 12px;
  height: 24px;
  background-color: var(--neon-cyan);
  animation: blink 1s step-end infinite;
}

.blinking-cursor-inline {
  display: inline-block;
  width: 10px;
  height: 1.1em;
  background-color: var(--neon-cyan);
  vertical-align: middle;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
</style>