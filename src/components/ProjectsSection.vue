<template>
  <section class="section-container">
    <div class="section-header">
      <div class="header-titles">
        <h2 class="section-title">Projects</h2>
        <p class="section-description">Selected software applications demonstrating full-stack engineering, distributed systems, and real-time telemetry.</p>
      </div>

      <!-- Category Filter Pills -->
      <div class="filter-pills" role="tablist" aria-label="Filter projects by discipline">
        <button 
          v-for="cat in categories" 
          :key="cat"
          :class="['filter-pill', { active: activeCategory === cat }]"
          @click="activeCategory = cat"
          role="tab"
          :aria-selected="activeCategory === cat"
        >
          {{ cat }}
          <span class="pill-count">{{ getCategoryCount(cat) }}</span>
        </button>
      </div>
    </div>

    <!-- Featured Showcase Project: Fight Hub (MMA Analytics) -->
    <div v-if="showFightHub" class="featured-project">
      <div class="featured-header">
        <div class="featured-meta">
          <span class="featured-badge">Featured System</span>
          <h3 class="featured-title">Fight Hub — MMA Analytics Engine</h3>
        </div>
        <div class="header-actions">
          <div class="tech-tags">
            <span class="tag">Vue.js</span>
            <span class="tag">Spring Boot</span>
            <span class="tag">Reactive Streams</span>
            <span class="tag">Telemetry</span>
          </div>
          <button 
            type="button" 
            class="specs-btn"
            @click="$emit('open-architecture', 'fight-hub')"
            title="Inspect system design and data schemas"
          >
            <svg class="specs-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M12 2 2 7l10 5 10-5-10-5Z"/>
              <path d="m2 17 10 5 10-5"/>
              <path d="m2 12 10 5 10-5"/>
            </svg>
            <span>Architecture Specs</span>
          </button>
        </div>
      </div>

      <p class="featured-desc">
        A real-time telemetry and statistical dashboard for mixed martial arts bouts. Aggregates round-by-round striking precision, target zone distribution, and positional grappling metrics into clean, interactive visual feeds.
      </p>

      <!-- The Craft Moment: Interactive MMA Telemetry Console -->
      <div class="telemetry-widget">
        <div class="telemetry-top">
          <div class="match-info">
            <span class="live-indicator"></span>
            <span class="match-title">Main Event · Lightweight Championship Bout (5 Rounds)</span>
          </div>

          <div class="round-tabs">
            <button 
              v-for="r in ['All', 'R1', 'R2', 'R3']" 
              :key="r"
              :class="['round-tab', { active: activeRound === r }]"
              @click="activeRound = r"
            >
              {{ r === 'All' ? 'Full Bout' : `Round ${r.slice(1)}` }}
            </button>
          </div>
        </div>

        <div class="fighters-bar">
          <div class="fighter f1">
            <span class="fighter-name">Fighter A (Striker)</span>
            <span class="fighter-stat">{{ currentStats.f1Total }} Significant Strikes ({{ currentStats.f1Accuracy }}% acc)</span>
          </div>
          <div class="stat-comparison-label">Striking & Grappling Telemetry</div>
          <div class="fighter f2">
            <span class="fighter-name">Fighter B (Grappler)</span>
            <span class="fighter-stat">{{ currentStats.f2Total }} Significant Strikes ({{ currentStats.f2Accuracy }}% acc)</span>
          </div>
        </div>

        <!-- Metric Output Bars -->
        <div class="metric-group">
          <div class="metric-row">
            <span class="metric-val left">{{ currentStats.f1Head }}%</span>
            <div class="bar-container">
              <div class="split-bar">
                <div class="bar-left" :style="{ width: `${currentStats.f1Head}%` }"></div>
                <div class="bar-right" :style="{ width: `${currentStats.f2Head}%` }"></div>
              </div>
              <span class="metric-name">Head Strike Accuracy</span>
            </div>
            <span class="metric-val right">{{ currentStats.f2Head }}%</span>
          </div>

          <div class="metric-row">
            <span class="metric-val left">{{ currentStats.f1Body }}</span>
            <div class="bar-container">
              <div class="split-bar">
                <div class="bar-left" :style="{ width: `${(currentStats.f1Body / 40) * 100}%` }"></div>
                <div class="bar-right" :style="{ width: `${(currentStats.f2Body / 40) * 100}%` }"></div>
              </div>
              <span class="metric-name">Body / Leg Damage</span>
            </div>
            <span class="metric-val right">{{ currentStats.f2Body }}</span>
          </div>

          <div class="metric-row">
            <span class="metric-val left">{{ currentStats.f1Takedowns }}</span>
            <div class="bar-container">
              <div class="split-bar">
                <div class="bar-left" :style="{ width: `${(currentStats.f1Takedowns / 6) * 100}%` }"></div>
                <div class="bar-right" :style="{ width: `${(currentStats.f2Takedowns / 6) * 100}%` }"></div>
              </div>
              <span class="metric-name">Takedowns Landed</span>
            </div>
            <span class="metric-val right">{{ currentStats.f2Takedowns }}</span>
          </div>
        </div>

        <!-- Target Zone Distribution Map -->
        <div class="zones-breakdown">
          <span class="zones-title">Target Zone Breakdown</span>
          <div class="zones-grid">
            <div class="zone-col">
              <span class="zone-label">Head Zone</span>
              <div class="zone-bar">
                <div class="zone-fill left" :style="{ width: `${currentStats.zoneF1.head}%` }"></div>
              </div>
              <span class="zone-meta">{{ currentStats.zoneF1.head }}% vs {{ currentStats.zoneF2.head }}%</span>
            </div>

            <div class="zone-col">
              <span class="zone-label">Body Zone</span>
              <div class="zone-bar">
                <div class="zone-fill mid" :style="{ width: `${currentStats.zoneF1.body}%` }"></div>
              </div>
              <span class="zone-meta">{{ currentStats.zoneF1.body }}% vs {{ currentStats.zoneF2.body }}%</span>
            </div>

            <div class="zone-col">
              <span class="zone-label">Leg / Low Kicks</span>
              <div class="zone-bar">
                <div class="zone-fill right" :style="{ width: `${currentStats.zoneF1.leg}%` }"></div>
              </div>
              <span class="zone-meta">{{ currentStats.zoneF1.leg }}% vs {{ currentStats.zoneF2.leg }}%</span>
            </div>
          </div>
        </div>

        <div class="telemetry-footer">
          <span class="telemetry-note">Reactive streams pipeline via Project Reactor & Spring Boot 3</span>
          <span class="telemetry-latency">Latency: 42ms · Sampled at 60Hz</span>
        </div>
      </div>
    </div>

    <!-- Secondary Projects Grid -->
    <div class="secondary-grid">
      <!-- Smart Stay -->
      <div v-if="matchesCategory('smart-stay')" class="project-card">
        <div class="card-inner-header">
          <div class="card-title-group">
            <h3 class="card-title">Smart Stay</h3>
            <span class="card-platform">Accommodation Platform</span>
          </div>
          <span class="status-chip">Booking Architecture</span>
        </div>

        <p class="card-description">
          A smart lodging and room reservation platform featuring real-time availability tracking, automated guest check-ins, and unified property management workflows.
        </p>

        <div class="feature-bullets">
          <div class="bullet">Architected room booking pipelines with conflict-free availability queries and booking state machines.</div>
          <div class="bullet">Designed an administrative portal for real-time occupancy monitoring, billing summaries, and room turnaround tracking.</div>
        </div>

        <div class="card-footer">
          <div class="tech-tags">
            <span class="tag">Vue.js</span>
            <span class="tag">Node.js</span>
            <span class="tag">Express.js</span>
            <span class="tag">PostgreSQL</span>
          </div>
          <button 
            type="button" 
            class="card-specs-link"
            @click="$emit('open-architecture', 'smart-stay')"
          >
            <span>Specs & Schemas →</span>
          </button>
        </div>
      </div>

      <!-- Attire Me -->
      <div v-if="matchesCategory('attire-me')" class="project-card">
        <div class="card-inner-header">
          <div class="card-title-group">
            <h3 class="card-title">Attire Me</h3>
            <span class="card-platform">iOS Application</span>
          </div>
          <span class="status-chip">Mobile Architecture</span>
        </div>

        <p class="card-description">
          An iOS outfit recommendation platform providing real-time personalized wardrobe suggestions based on live weather data, local forecast, and user preference algorithms.
        </p>

        <div class="feature-bullets">
          <div class="bullet">Integrated weather API endpoints for dynamic context-aware clothing suggestions.</div>
          <div class="bullet">Engineered community wardrobe sharing with optimized media caching via Cloudinary and Supabase.</div>
        </div>

        <div class="card-footer">
          <div class="tech-tags">
            <span class="tag">Swift</span>
            <span class="tag">Supabase</span>
            <span class="tag">Cloudinary</span>
            <span class="tag">REST API</span>
          </div>
          <button 
            type="button" 
            class="card-specs-link"
            @click="$emit('open-architecture', 'attire-me')"
          >
            <span>Specs & Schemas →</span>
          </button>
        </div>
      </div>

      <!-- BringIt -->
      <div v-if="matchesCategory('bring-it')" class="project-card">
        <div class="card-inner-header">
          <div class="card-title-group">
            <h3 class="card-title">BringIt</h3>
            <span class="card-platform">Full-Stack Web App</span>
          </div>
          <span class="status-chip">Quick-Commerce</span>
        </div>

        <p class="card-description">
          A high-concurrency quick-commerce web application featuring real-time catalog browsing, shopping cart synchronization, and secure JWT-based customer authentication.
        </p>

        <div class="feature-bullets">
          <div class="bullet">Built modular React components with responsive product catalogs and instantaneous filtering.</div>
          <div class="bullet">Architected Express.js REST endpoints with MongoDB aggregation pipelines for rapid inventory lookups.</div>
        </div>

        <div class="card-footer">
          <div class="tech-tags">
            <span class="tag">React.js</span>
            <span class="tag">Node.js</span>
            <span class="tag">Express.js</span>
            <span class="tag">MongoDB</span>
          </div>
          <button 
            type="button" 
            class="card-specs-link"
            @click="$emit('open-architecture', 'bring-it')"
          >
            <span>Specs & Schemas →</span>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

defineEmits(['open-architecture'])

const activeRound = ref('All')
const activeCategory = ref('All')

const categories = ['All', 'Full-Stack', 'Frontend & Telemetry', 'Mobile iOS']

const projectCategories = {
  'fight-hub': ['All', 'Full-Stack', 'Frontend & Telemetry'],
  'smart-stay': ['All', 'Full-Stack'],
  'attire-me': ['All', 'Mobile iOS'],
  'bring-it': ['All', 'Full-Stack']
}

const getCategoryCount = (cat) => {
  if (cat === 'All') return 4
  return Object.values(projectCategories).filter(cats => cats.includes(cat)).length
}

const showFightHub = computed(() => {
  return projectCategories['fight-hub'].includes(activeCategory.value)
})

const matchesCategory = (projId) => {
  return projectCategories[projId].includes(activeCategory.value)
}

const statsData = {
  All: { 
    f1Total: 142, f2Total: 108, f1Accuracy: 67, f2Accuracy: 52,
    f1Head: 64, f2Head: 48, f1Body: 34, f2Body: 22, f1Takedowns: 1, f2Takedowns: 5,
    zoneF1: { head: 62, body: 24, leg: 14 },
    zoneF2: { head: 44, body: 28, leg: 28 }
  },
  R1: { 
    f1Total: 48, f2Total: 31, f1Accuracy: 72, f2Accuracy: 45,
    f1Head: 72, f2Head: 45, f1Body: 12, f2Body: 8, f1Takedowns: 0, f2Takedowns: 1,
    zoneF1: { head: 70, body: 18, leg: 12 },
    zoneF2: { head: 40, body: 30, leg: 30 }
  },
  R2: { 
    f1Total: 52, f2Total: 34, f1Accuracy: 68, f2Accuracy: 50,
    f1Head: 68, f2Head: 50, f1Body: 14, f2Body: 6, f1Takedowns: 1, f2Takedowns: 2,
    zoneF1: { head: 64, body: 24, leg: 12 },
    zoneF2: { head: 46, body: 26, leg: 28 }
  },
  R3: { 
    f1Total: 42, f2Total: 43, f1Accuracy: 52, f2Accuracy: 49,
    f1Head: 52, f2Head: 49, f1Body: 8, f2Body: 8, f1Takedowns: 0, f2Takedowns: 2,
    zoneF1: { head: 50, body: 32, leg: 18 },
    zoneF2: { head: 48, body: 28, leg: 24 }
  }
}

const currentStats = computed(() => statsData[activeRound.value])
</script>

<style scoped>
.section-container {
  margin-bottom: 56px;
}

.section-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 28px;
  flex-wrap: wrap;
}

.header-titles {
  max-width: 600px;
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

/* Category Filter Pills */
.filter-pills {
  display: flex;
  align-items: center;
  gap: 6px;
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  padding: 3px;
  border-radius: var(--radius-md);
  flex-wrap: wrap;
}

.filter-pill {
  background: transparent;
  border: none;
  font-size: 12px;
  font-family: var(--font-sans);
  color: var(--text-secondary);
  padding: 5px 12px;
  border-radius: 6px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  transition: all 120ms var(--ease-standard);
}

.filter-pill:hover {
  color: var(--text-primary);
}

.filter-pill.active {
  background-color: var(--bg-surface-raised);
  color: var(--text-primary);
  font-weight: 500;
}

.pill-count {
  font-size: 10px;
  font-family: var(--font-mono);
  color: var(--text-muted);
}

.filter-pill.active .pill-count {
  color: var(--accent);
}

/* Featured Project Card */
.featured-project {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-xl);
  padding: 28px;
  margin-bottom: 24px;
  transition: border-color 140ms var(--ease-standard);
}

.featured-project:hover {
  border-color: var(--border-hover);
}

.featured-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 12px;
  flex-wrap: wrap;
}

.featured-meta {
  display: flex;
  flex-direction: column;
}

.featured-badge {
  display: inline-block;
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--accent);
  background-color: var(--accent-muted);
  border: 1px solid var(--accent-border);
  padding: 2px 8px;
  border-radius: var(--radius-sm);
  margin-bottom: 8px;
  align-self: flex-start;
}

.featured-title {
  margin: 0;
  font-size: 18px;
  font-weight: 600;
  color: var(--text-primary);
  letter-spacing: -0.01em;
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
}

.specs-btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-sm);
  padding: 5px 10px;
  font-size: 12px;
  color: var(--text-primary);
  cursor: pointer;
  transition: all 120ms var(--ease-standard);
}

.specs-btn:hover {
  border-color: var(--border-hover);
  background-color: var(--bg-surface-hover);
}

.specs-icon {
  width: 14px;
  height: 14px;
  color: var(--accent);
}

.featured-desc {
  margin: 0 0 24px;
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.6;
  max-width: 820px;
}

/* Craft Moment: Telemetry Widget */
.telemetry-widget {
  background-color: var(--telemetry-bg);
  border: 1px solid var(--telemetry-border);
  border-radius: var(--radius-lg);
  padding: 20px;
  transition: background-color 180ms var(--ease-standard), border-color 180ms var(--ease-standard);
}

.telemetry-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-bottom: 14px;
  border-bottom: 1px solid var(--border-hairline);
  margin-bottom: 16px;
  flex-wrap: wrap;
  gap: 12px;
}

.match-info {
  display: flex;
  align-items: center;
  gap: 8px;
}

.live-indicator {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background-color: var(--accent);
}

.match-title {
  font-size: 12px;
  font-weight: 500;
  color: var(--text-secondary);
  font-family: var(--font-mono);
}

.round-tabs {
  display: flex;
  gap: 4px;
  background-color: var(--telemetry-box);
  padding: 3px;
  border-radius: var(--radius-sm);
  border: 1px solid var(--telemetry-border);
}

.round-tab {
  background: transparent;
  border: none;
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--text-muted);
  padding: 4px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: all 120ms var(--ease-standard);
}

.round-tab:hover {
  color: var(--text-primary);
}

.round-tab.active {
  background-color: var(--bg-surface);
  color: var(--text-primary);
  font-weight: 500;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}

.fighters-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 18px;
  font-size: 12px;
}

.fighter {
  display: flex;
  flex-direction: column;
}

.fighter.f1 {
  align-items: flex-start;
}

.fighter.f2 {
  align-items: flex-end;
}

.fighter-name {
  font-weight: 600;
  color: var(--text-primary);
}

.fighter-stat {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--accent);
}

.stat-comparison-label {
  font-size: 11px;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* Metric Bars */
.metric-group {
  display: flex;
  flex-direction: column;
  gap: 14px;
  margin-bottom: 20px;
}

.metric-row {
  display: grid;
  grid-template-columns: 44px 1fr 44px;
  align-items: center;
  gap: 12px;
}

.metric-val {
  font-size: 12px;
  font-family: var(--font-mono);
  font-weight: 500;
  color: var(--text-primary);
  font-variant-numeric: tabular-nums;
}

.metric-val.left {
  text-align: right;
  color: var(--accent);
}

.metric-val.right {
  text-align: left;
  color: var(--text-secondary);
}

.bar-container {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.metric-name {
  font-size: 11px;
  color: var(--text-muted);
  text-align: center;
}

.split-bar {
  height: 6px;
  background-color: var(--telemetry-track);
  border-radius: 9999px;
  display: flex;
  overflow: hidden;
  gap: 2px;
}

.bar-left {
  background-color: var(--accent);
  height: 100%;
  border-radius: 9999px 0 0 9999px;
  transition: width 240ms var(--ease-standard);
}

.bar-right {
  background-color: var(--text-muted);
  height: 100%;
  border-radius: 0 9999px 9999px 0;
  margin-left: auto;
  transition: width 240ms var(--ease-standard);
}

/* Target Zone Breakdown */
.zones-breakdown {
  background-color: var(--telemetry-box);
  border: 1px solid var(--telemetry-border);
  border-radius: var(--radius-sm);
  padding: 12px 14px;
  margin-bottom: 16px;
}

.zones-title {
  display: block;
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.04em;
  margin-bottom: 10px;
}

.zones-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.zone-col {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.zone-label {
  font-size: 11px;
  color: var(--text-secondary);
  font-weight: 500;
}

.zone-bar {
  height: 4px;
  background-color: var(--telemetry-track);
  border-radius: 2px;
  overflow: hidden;
}

.zone-fill {
  height: 100%;
  background-color: var(--accent);
  border-radius: 2px;
  transition: width 240ms var(--ease-standard);
}

.zone-meta {
  font-size: 10.5px;
  font-family: var(--font-mono);
  color: var(--text-muted);
}

.telemetry-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 12px;
  border-top: 1px solid var(--border-hairline);
  font-size: 11px;
  color: var(--text-muted);
  font-family: var(--font-mono);
  flex-wrap: wrap;
  gap: 8px;
}

/* Secondary Grid */
.secondary-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.project-card {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-lg);
  padding: 24px;
  display: flex;
  flex-direction: column;
  transition: border-color 140ms var(--ease-standard);
}

.project-card:hover {
  border-color: var(--border-hover);
}

.card-inner-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 12px;
}

.card-title-group {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.card-title {
  margin: 0;
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
  letter-spacing: -0.01em;
}

.card-platform {
  font-size: 12px;
  color: var(--text-muted);
}

.status-chip {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--text-secondary);
  background-color: var(--bg-surface-raised);
  padding: 2px 8px;
  border-radius: var(--radius-sm);
  white-space: nowrap;
}

.card-description {
  margin: 0 0 16px;
  font-size: 13px;
  color: var(--text-secondary);
  line-height: 1.55;
  flex: 1;
}

.feature-bullets {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
}

.bullet {
  font-size: 12px;
  color: var(--text-muted);
  line-height: 1.5;
  position: relative;
  padding-left: 12px;
}

.bullet::before {
  content: '·';
  position: absolute;
  left: 2px;
  top: -1px;
  font-size: 16px;
  color: var(--accent);
}

/* Card Footer */
.card-footer {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: auto;
  padding-top: 14px;
  border-top: 1px solid var(--border-hairline);
}

.card-specs-link {
  background: transparent;
  border: none;
  padding: 0;
  font-size: 12px;
  font-family: var(--font-mono);
  color: var(--accent);
  cursor: pointer;
  align-self: flex-start;
  transition: color 120ms var(--ease-standard);
}

.card-specs-link:hover {
  color: var(--text-primary);
  text-decoration: underline;
}

/* Tech Tags */
.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--text-secondary);
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  padding: 2px 8px;
  border-radius: 4px;
}

@media (max-width: 960px) {
  .secondary-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  }
}

@media (max-width: 640px) {
  .secondary-grid {
    grid-template-columns: 1fr;
  }
  .zones-grid {
    grid-template-columns: 1fr;
  }
}
</style>
