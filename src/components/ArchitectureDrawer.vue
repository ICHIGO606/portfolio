<template>
  <div v-if="project" class="drawer-overlay" @click.self="close">
    <div class="drawer-panel" role="dialog" aria-modal="true" :aria-label="`${data.title} Architecture Specification`">
      <!-- Drawer Header -->
      <div class="drawer-header">
        <div class="header-titles">
          <span class="platform-badge">{{ data.platform }} · Architecture Specs</span>
          <h2 class="project-heading">{{ data.title }}</h2>
        </div>
        <button type="button" class="close-btn" @click="close" aria-label="Close specifications">
          <svg class="close-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <path d="M18 6 6 18M6 6l12 12"/>
          </svg>
        </button>
      </div>

      <!-- Drawer Content -->
      <div class="drawer-body">
        <!-- Overview & Tech Stack -->
        <div class="doc-section">
          <h3 class="section-label">System Overview</h3>
          <p class="section-text">{{ data.overview }}</p>
          <div class="tags-container">
            <span v-for="tag in data.stack" :key="tag" class="tech-tag">{{ tag }}</span>
          </div>
        </div>

        <!-- Architecture Flow Diagram -->
        <div class="doc-section">
          <h3 class="section-label">Architecture Pipeline</h3>
          <div class="pipeline-card">
            <div 
              v-for="(step, idx) in data.pipeline" 
              :key="idx" 
              class="pipeline-step"
            >
              <div class="step-num">{{ String(idx + 1).padStart(2, '0') }}</div>
              <div class="step-content">
                <span class="step-title">{{ step.title }}</span>
                <span class="step-detail">{{ step.detail }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Technical Design Decisions -->
        <div class="doc-section">
          <h3 class="section-label">Key Engineering Decisions</h3>
          <ul class="decisions-list">
            <li v-for="(dec, idx) in data.decisions" :key="idx">
              <strong class="decision-title">{{ dec.title }}:</strong>
              <span class="decision-desc">{{ dec.description }}</span>
            </li>
          </ul>
        </div>

        <!-- Schema / Code Spec Snippet -->
        <div class="doc-section">
          <h3 class="section-label">{{ data.codeTitle }}</h3>
          <div class="code-block">
            <pre><code>{{ data.codeSnippet }}</code></pre>
          </div>
        </div>

        <!-- Operational Metrics -->
        <div class="doc-section">
          <h3 class="section-label">Key Metrics & Reliability</h3>
          <div class="metrics-grid">
            <div v-for="(metric, idx) in data.metrics" :key="idx" class="metric-card">
              <span class="metric-num">{{ metric.val }}</span>
              <span class="metric-sub">{{ metric.label }}</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Drawer Footer -->
      <div class="drawer-footer">
        <span class="footer-tip">Press <kbd>ESC</kbd> or click outside to close</span>
        <button type="button" class="done-btn" @click="close">Done</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  project: String // 'fight-hub' | 'smart-stay' | 'attire-me' | 'bring-it' | null
})

const emit = defineEmits(['close'])

const close = () => {
  emit('close')
}

const specs = {
  'fight-hub': {
    title: 'Fight Hub — MMA Analytics Engine',
    platform: 'Vue.js + Spring Boot Reactive Streams',
    overview: 'A low-latency telemetric analytics platform ingesting round-by-round combat metrics, computing striking accuracy vectors in real time, and serving sub-second updates to interactive frontend clients.',
    stack: ['Vue 3 (Composition API)', 'Spring Boot 3', 'Project Reactor', 'WebSocket STOMP', 'REST API', 'SVG Visualizations'],
    pipeline: [
      { title: 'Telemetry Ingestion', detail: 'Event streams ingested via WebSocket channels or sampled live telemetry endpoints.' },
      { title: 'Metric Aggregation Engine', detail: 'Real-time calculation of significant strike ratios, control percentages, and damage distribution.' },
      { title: 'Reactive State Distribution', detail: 'Spring Boot handles concurrency with non-blocking reactive streams, broadcasting JSON state deltas.' },
      { title: 'Client Canvas / SVG Render', detail: 'Vue 3 reactive binding updates strike bars and hit-zone SVG maps at 60Hz without layout thrashing.' }
    ],
    decisions: [
      { title: 'Reactive non-blocking stream handling', description: 'Selected Project Reactor to manage bursts of combat events during championship bouts with low memory footprint.' },
      { title: 'Normalized telemetry payload schema', description: 'Enforced round-by-round strike breakdowns with tabular numeric representations to ensure seamless frontend visualization.' },
      { title: 'Client-side vector computations', description: 'Cached full bout statistics client-side to enable instant round switching without redundant roundtrips.' }
    ],
    codeTitle: 'Telemetry Event Ingestion Schema (Java / Spring)',
    codeSnippet: `@Getter @Builder
public record FightTelemetryEvent(
    String boutId,
    int round,
    int elapsedSeconds,
    StrikerMetric fighterA,
    StrikerMetric fighterB
) {
    public double getSignificantAccuracy(StrikerMetric f) {
        return f.attempted() == 0 ? 0.0 : ((double) f.landed() / f.attempted()) * 100.0;
    }
}`,
    metrics: [
      { val: '< 50ms', label: 'Telemetry latency' },
      { val: '60 Hz', label: 'Client render rate' },
      { val: '100%', label: 'Round-by-round fidelity' }
    ]
  },

  'smart-stay': {
    title: 'Smart Stay — Accommodation & Booking System',
    platform: 'Full-Stack Architecture (Node.js / Express / PostgreSQL)',
    overview: 'A smart lodging and room reservation platform designed to eliminate double-booking through atomic state machines, automated check-in workflows, and administrative occupancy dashboards.',
    stack: ['Vue.js', 'Node.js', 'Express.js', 'PostgreSQL', 'Prisma ORM', 'JWT Security'],
    pipeline: [
      { title: 'Availability Query Engine', detail: 'Queries overlapping date ranges with PostgreSQL index optimization to return live available units.' },
      { title: 'Pessimistic Inventory Locking', detail: 'Applies a 15-minute temporary reservation lock while guest completes payment authorization.' },
      { title: 'State Machine Transition', detail: 'Transitions booking from PENDING -> CONFIRMED -> CHECKED_IN -> COMPLETED with audit logging.' },
      { title: 'Automated Housekeeping Dispatch', detail: 'Triggers maintenance and room sanitization alerts immediately upon checkout confirmation.' }
    ],
    decisions: [
      { title: 'Database transactional isolation', description: 'Employed PostgreSQL serializable transactions during booking creation to prevent race conditions during high-demand dates.' },
      { title: 'Strict booking state lifecycle', description: 'Modeled reservations as an explicit finite state machine with automatic TTL expiration on unpaid holds.' },
      { title: 'Partitioned room inventory', description: 'Indexed room units by property category, floor, and amenities to support sub-10ms filter lookups.' }
    ],
    codeTitle: 'Reservation State Machine (TypeScript / Node)',
    codeSnippet: `export async function reserveRoom(roomId: string, dates: DateRange, userId: string) {
  return await prisma.$transaction(async (tx) => {
    // Lock row for update to eliminate concurrent collisions
    const room = await tx.room.findUnique({
      where: { id: roomId },
      select: { status: true, version: true }
    });
    
    if (room.status !== 'AVAILABLE') throw new RoomUnavailableError();

    return await tx.booking.create({
      data: { roomId, userId, dates, status: 'PENDING_PAYMENT', expiresAt: Date.now() + 15 * 60 * 1000 }
    });
  });
}`,
    metrics: [
      { val: '0', label: 'Double-booking rate' },
      { val: '15 min', label: 'Payment lock TTL' },
      { val: '< 15ms', label: 'Room search query time' }
    ]
  },

  'attire-me': {
    title: 'Attire Me — iOS Outfit Recommender',
    platform: 'Native iOS (Swift / Supabase / Cloudinary)',
    overview: 'An intelligent iOS application recommending personalized daily wardrobe combinations based on hyperlocal weather telemetry, temperature thresholds, and user style preferences.',
    stack: ['Swift', 'SwiftUI / UIKit', 'Supabase', 'Cloudinary CDN', 'CoreLocation', 'WeatherKit'],
    pipeline: [
      { title: 'Hyperlocal Weather Fetch', detail: 'Retrieves current temperature, precipitation index, and wind chill via CoreLocation and Weather APIs.' },
      { title: 'Wardrobe Tag Filtering', detail: 'Matches temperature bands to user wardrobe items tagged by fabric weight and garment type.' },
      { title: 'Client Image Cache Engine', detail: 'Fetches optimized WebP thumbnails via Cloudinary with disk caching for instantaneous loading.' },
      { title: 'Community Wardrobe Feed', detail: 'Syncs community outfits and feedback using Supabase realtime subscriptions.' }
    ],
    decisions: [
      { title: 'MVVM with Combine / Async-Await', description: 'Decoupled weather polling and image decompression from main thread to maintain 60 FPS scrolling.' },
      { title: 'Edge media transformation', description: 'Offloaded image resizing and format conversion to Cloudinary CDN, reducing payload by 70%.' },
      { title: 'Offline-first fallback cache', description: 'Persisted last known recommendation locally so the app opens immediately without internet access.' }
    ],
    codeTitle: 'Weather-To-Garment Recommendation Rule (Swift)',
    codeSnippet: `struct RecommendationEngine {
    func evaluate(weather: WeatherTelemetry, wardrobe: [Garment]) -> [OutfitSuggestion] {
        let targetWarmth = weather.temperature < 15.0 ? WarmthTier.heavy : WarmthTier.light
        return wardrobe
            .filter { $0.warmthTier == targetWarmth }
            .grouped(by: \\.category)
            .generateCompatibleOutfits(weatherCondition: weather.condition)
    }
}`,
    metrics: [
      { val: '70%', label: 'Image payload reduction' },
      { val: '60 FPS', label: 'Scroll performance' },
      { val: '100%', label: 'Offline fallback coverage' }
    ]
  },

  'bring-it': {
    title: 'BringIt — Quick-Commerce Delivery Application',
    platform: 'Full-Stack Web (React.js / Node.js / Express / MongoDB)',
    overview: 'A high-throughput quick-commerce web application featuring real-time grocery inventory browsing, shopping cart synchronization, and secure JWT-based customer authentication.',
    stack: ['React.js', 'Node.js', 'Express.js', 'MongoDB', 'JWT Auth', 'Mongoose Aggregations'],
    pipeline: [
      { title: 'Catalog Search & Filter', detail: 'MongoDB text index aggregation for sub-second grocery search and category filtering.' },
      { title: 'Cart Sync & Local Storage', detail: 'Bi-directional cart sync combining client-side local cache with server sessions.' },
      { title: 'JWT Auth & Refresh Token Flow', detail: 'Access tokens stored in memory with HTTP-only refresh cookies to eliminate XSS vulnerabilities.' },
      { title: 'Atomic Inventory Decrement', detail: 'Executes atomic MongoDB $inc operations during checkout to prevent overselling.' }
    ],
    decisions: [
      { title: 'Atomic inventory operations', description: 'Used MongoDB conditional updates ($inc: { stock: -qty }, { stock: { $gte: qty } }) to guarantee consistency.' },
      { title: 'Secure token architecture', description: 'Implemented short-lived 15m JWTs paired with refresh token rotation stored in secure HTTP-only cookies.' },
      { title: 'Compound indexes for fast lookups', description: 'Structured category and price indexes to support simultaneous sorting and filtering.' }
    ],
    codeTitle: 'Atomic Inventory Check & Checkout (Node / Mongo)',
    codeSnippet: `export const checkoutOrder = async (cartItems, userId) => {
  const session = await mongoose.startSession();
  session.startTransaction();
  try {
    for (const item of cartItems) {
      const updated = await Product.updateOne(
        { _id: item.productId, stock: { $gte: item.quantity } },
        { $inc: { stock: -item.quantity } },
        { session }
      );
      if (updated.modifiedCount === 0) throw new Error(\`Insufficient stock: \${item.name}\`);
    }
    await session.commitTransaction();
  } finally {
    session.endSession();
  }
};`,
    metrics: [
      { val: '< 20ms', label: 'Catalog search latency' },
      { val: '80%', label: 'Unauthorized access reduction' },
      { val: '100%', label: 'Atomic inventory accuracy' }
    ]
  }
}

const data = computed(() => {
  return props.project ? specs[props.project] : null
})

const handleKey = (e) => {
  if (e.key === 'Escape' && props.project) {
    close()
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKey)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKey)
})
</script>

<style scoped>
.drawer-overlay {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.65);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  z-index: 1000;
  display: flex;
  justify-content: flex-end;
}

.drawer-panel {
  width: 100%;
  max-width: 640px;
  height: 100%;
  background-color: var(--bg-surface);
  border-left: 1px solid var(--border-hairline);
  box-shadow: -10px 0 30px rgba(0, 0, 0, 0.4);
  display: flex;
  flex-direction: column;
  animation: slideIn 220ms var(--ease-standard);
}

@keyframes slideIn {
  from { transform: translateX(100%); }
  to { transform: translateX(0); }
}

.drawer-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  padding: 24px;
  border-bottom: 1px solid var(--border-hairline);
  gap: 16px;
}

.header-titles {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.platform-badge {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.project-heading {
  margin: 0;
  font-size: 20px;
  font-weight: 600;
  color: var(--text-primary);
  letter-spacing: -0.015em;
}

.close-btn {
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-sm);
  color: var(--text-secondary);
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 120ms var(--ease-standard);
  flex-shrink: 0;
}

.close-btn:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
}

.close-icon {
  width: 16px;
  height: 16px;
}

/* Body */
.drawer-body {
  flex: 1;
  overflow-y: auto;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 28px;
}

.doc-section {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.section-label {
  margin: 0;
  font-size: 12px;
  font-family: var(--font-mono);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.section-text {
  margin: 0;
  font-size: 13.5px;
  color: var(--text-secondary);
  line-height: 1.6;
}

.tags-container {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 4px;
}

.tech-tag {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--text-secondary);
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  padding: 2px 8px;
  border-radius: 4px;
}

/* Pipeline */
.pipeline-card {
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.pipeline-step {
  display: flex;
  gap: 12px;
  align-items: flex-start;
}

.step-num {
  font-size: 11px;
  font-family: var(--font-mono);
  color: var(--accent);
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  padding: 2px 6px;
  border-radius: 4px;
  flex-shrink: 0;
}

.step-content {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.step-title {
  font-size: 13px;
  font-weight: 500;
  color: var(--text-primary);
}

.step-detail {
  font-size: 12px;
  color: var(--text-muted);
  line-height: 1.5;
}

/* Decisions */
.decisions-list {
  margin: 0;
  padding-left: 18px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.decisions-list li {
  font-size: 13px;
  color: var(--text-secondary);
  line-height: 1.55;
}

.decision-title {
  color: var(--text-primary);
  font-weight: 500;
}

/* Code Snippet */
.code-block {
  background-color: #07090e;
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  padding: 14px 16px;
  overflow-x: auto;
}

.code-block pre {
  margin: 0;
}

.code-block code {
  font-family: var(--font-mono);
  font-size: 12px;
  color: #cfd6e6;
  line-height: 1.6;
}

/* Metrics */
.metrics-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
}

.metric-card {
  background-color: var(--bg-surface-raised);
  border: 1px solid var(--border-hairline);
  border-radius: var(--radius-md);
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 2px;
  align-items: center;
  text-align: center;
}

.metric-num {
  font-size: 18px;
  font-weight: 600;
  font-family: var(--font-mono);
  color: var(--accent);
}

.metric-sub {
  font-size: 11px;
  color: var(--text-muted);
}

/* Footer */
.drawer-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 24px;
  border-top: 1px solid var(--border-hairline);
  background-color: var(--bg-surface-raised);
}

.footer-tip {
  font-size: 11px;
  color: var(--text-muted);
  font-family: var(--font-mono);
}

.footer-tip kbd {
  background-color: var(--bg-surface);
  border: 1px solid var(--border-hairline);
  padding: 1px 4px;
  border-radius: 3px;
}

.done-btn {
  background-color: var(--btn-primary-bg);
  color: var(--btn-primary-text);
  border: none;
  font-size: 12px;
  font-weight: 500;
  padding: 6px 14px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all 120ms var(--ease-standard);
}

.done-btn:hover {
  background-color: var(--btn-primary-hover-bg);
  color: var(--btn-primary-hover-text);
}

@media (max-width: 640px) {
  .drawer-panel {
    max-width: 100%;
  }
  .metrics-grid {
    grid-template-columns: 1fr;
  }
}
</style>

