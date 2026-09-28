<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref, watch } from 'vue'
import { useNav } from '@slidev/client'

type TimerState = {
  totalElapsed: number
  slideElapsed: number[]
  tickStarted: number | null
  activeSlide: number
}

const sections = [
  { from: 1, to: 3, label: 'WHY' },
  { from: 4, to: 5, label: 'OVERVIEW' },
  { from: 6, to: 8, label: 'BEFORE' },
  { from: 9, to: 15, label: 'SHOP 6' },
  { from: 16, to: 18, label: 'COMPARE' },
  { from: 19, to: 19, label: 'DISCUSS' },
  { from: 20, to: 21, label: 'TRY + CLOSE' },
]
// Per-slide budgets total 60 minutes. The extra two minutes support the
// second live demo's review and documentation steps.
const slideMinutes = [1, 2, 2, 3, 2, 0.5, 3, 2, 0.5, 3, 4, 4, 4, 3, 2, 2, 2, 2, 3, 14, 1]
const totalMinutes = 60
const storageKey = 'shop6-agentic-workshop-timer-v5'
const nav = useNav()
const now = ref(Date.now())
const slideNumber = computed(() => Math.min(slideMinutes.length, Math.max(1, nav.currentSlideNo.value)))
const sectionIndex = computed(() => Math.max(0, sections.findIndex(section => slideNumber.value >= section.from && slideNumber.value <= section.to)))

function freshState(): TimerState {
  return { totalElapsed: 0, slideElapsed: slideMinutes.map(() => 0), tickStarted: Date.now(), activeSlide: slideNumber.value }
}

function loadState(): TimerState {
  try {
    const saved = JSON.parse(localStorage.getItem(storageKey) || '') as Partial<TimerState>
    if (typeof saved.totalElapsed === 'number' && Array.isArray(saved.slideElapsed)) {
      return {
        totalElapsed: saved.totalElapsed,
        slideElapsed: slideMinutes.map((_, index) => Number(saved.slideElapsed?.[index]) || 0),
        tickStarted: typeof saved.tickStarted === 'number' ? saved.tickStarted : null,
        activeSlide: Math.min(slideMinutes.length, Math.max(1, Number(saved.activeSlide) || 1)),
      }
    }
  } catch { /* First visit or unavailable local storage. */ }
  return freshState()
}

const state = ref<TimerState>(freshState())
const runningElapsed = computed(() => state.value.tickStarted === null ? 0 : Math.max(0, now.value - state.value.tickStarted))
const activeSlideElapsed = computed(() => state.value.slideElapsed[slideNumber.value - 1]
  + (state.value.activeSlide === slideNumber.value ? runningElapsed.value : 0))
const slideRemaining = computed(() => slideMinutes[slideNumber.value - 1] * 60_000 - activeSlideElapsed.value)
const slideProgress = computed(() => activeSlideElapsed.value / (slideMinutes[slideNumber.value - 1] * 60_000))
const totalRemaining = computed(() => totalMinutes * 60_000 - state.value.totalElapsed - runningElapsed.value)
const slideRingProgress = computed(() => Math.min(1, Math.max(0, 1 - slideProgress.value)))
const totalProgress = computed(() => (state.value.totalElapsed + runningElapsed.value) / (totalMinutes * 60_000))
const totalRingProgress = computed(() => Math.min(1, Math.max(0, totalProgress.value)))
const totalWarningClass = computed(() => {
  if (totalProgress.value >= 1) return 'warning-red'
  if (totalProgress.value >= 0.85) return 'warning-orange'
  if (totalProgress.value >= 0.7) return 'warning-yellow'
  return ''
})
const warningClass = computed(() => {
  if (slideRemaining.value < 0 || totalRemaining.value < 0 || slideProgress.value >= 1) return 'warning-red'
  if (slideProgress.value >= 0.85) return 'warning-orange'
  if (slideProgress.value >= 0.7) return 'warning-yellow'
  return ''
})
const warningText = computed(() => {
  if (slideRemaining.value < 0) return 'SLIDE OVER'
  if (totalRemaining.value < 0) return 'TOTAL OVER'
  if (slideProgress.value >= 0.85) return 'NEAR LIMIT'
  if (slideProgress.value >= 0.7) return 'TIME CHECK'
  return ''
})
const sectionRemaining = (section: typeof sections[number], index: number) => {
  const budget = slideMinutes.slice(section.from - 1, section.to).reduce((sum, minutes) => sum + minutes * 60_000, 0)
  const elapsed = state.value.slideElapsed.slice(section.from - 1, section.to).reduce((sum, milliseconds) => sum + milliseconds, 0)
    + (sectionIndex.value === index && state.value.activeSlide === slideNumber.value ? runningElapsed.value : 0)
  return budget - elapsed
}
const slideText = computed(() => formatRemaining(slideRemaining.value))
const totalText = computed(() => formatRemaining(totalRemaining.value))
const timeline = computed(() => sections.map((section, index) => {
  const budget = slideMinutes.slice(section.from - 1, section.to).reduce((sum, minutes) => sum + minutes * 60_000, 0)
  const remaining = sectionRemaining(section, index)
  const elapsed = budget - remaining
  return {
    ...section,
    remaining,
    remainingText: formatRemaining(remaining),
    progress: Math.min(100, Math.max(0, elapsed / budget * 100)),
    overdue: index === sectionIndex.value && remaining < 0,
    current: index === sectionIndex.value,
  }
}))

function formatRemaining(milliseconds: number) {
  const seconds = Math.floor(Math.abs(milliseconds) / 1000)
  const clock = `${String(Math.floor(seconds / 60)).padStart(2, '0')}:${String(seconds % 60).padStart(2, '0')}`
  return milliseconds < 0 ? `+${clock}` : clock
}

function persist() {
  try { localStorage.setItem(storageKey, JSON.stringify(state.value)) } catch { /* Timer remains usable without storage. */ }
}

function commit(at: number) {
  const started = state.value.tickStarted
  if (started === null) return
  const elapsed = Math.max(0, at - started)
  state.value.totalElapsed += elapsed
  state.value.slideElapsed[state.value.activeSlide - 1] += elapsed
  state.value.tickStarted = at
}

function reset() {
  if (state.value.totalElapsed > 0 && !window.confirm('Reset the workshop timer?')) return
  state.value = freshState()
  persist()
}

watch(slideNumber, (nextSlide) => {
  if (nextSlide === state.value.activeSlide) return
  const at = Date.now()
  commit(at)
  state.value.activeSlide = nextSlide
  state.value.tickStarted = at
  persist()
}, { flush: 'sync' })

function syncFromStorage(event: StorageEvent) {
  if (event.key !== storageKey || !event.newValue) return
  try { state.value = JSON.parse(event.newValue) as TimerState } catch { /* Ignore malformed updates. */ }
}

let heartbeat: number | undefined
onMounted(() => {
  state.value = loadState()
  // Resume persisted elapsed time on the slide that was active before reload,
  // then begin (or continue) timing the slide currently open.
  if (state.value.tickStarted !== null) commit(Date.now())
  state.value.activeSlide = slideNumber.value
  state.value.tickStarted = Date.now()
  persist()
  heartbeat = window.setInterval(() => { now.value = Date.now() }, 250)
  window.addEventListener('storage', syncFromStorage)
})
onBeforeUnmount(() => {
  if (heartbeat) window.clearInterval(heartbeat)
  window.removeEventListener('storage', syncFromStorage)
})
</script>

<template>
  <aside class="workshop-timer" :class="warningClass" aria-label="Current slide and total workshop timer" @pointerdown.stop @touchstart.stop>
    <div class="timer-gauge" role="img" :aria-label="`Total remaining ${totalText}; slide ${slideNumber} remaining ${slideText}`">
      <div class="gauge-total" :class="totalWarningClass" :style="{ '--progress': `${totalRingProgress * 100}%` }">
        <div class="gauge-slide" :class="warningClass" :style="{ '--progress': `${slideRingProgress * 100}%` }">
          <strong :class="{ overtime: slideRemaining < 0 }">{{ slideText }}</strong>
        </div>
      </div>
    </div>
    <div class="timer-readout">
      <div class="clock-group"><span class="clock-label">TOTAL</span><strong :class="{ overtime: totalRemaining < 0 }">{{ totalText }}</strong></div>
      <div class="clock-group"><span class="clock-label">SLIDE {{ slideNumber }}/{{ slideMinutes.length }}</span><span v-if="warningText" class="overdue-label">{{ warningText }}</span></div>
    </div>
    <button class="timer-reset" aria-label="Reset workshop timer" @click.stop="reset">↺</button>
  </aside>
  <nav class="workshop-timeline" aria-label="Workshop section timeline" @pointerdown.stop @touchstart.stop>
    <div
      v-for="(section, index) in timeline"
      :key="section.label"
      class="timeline-section"
      :class="{ current: section.current, overdue: section.overdue }"
      :style="{ flexGrow: 1 }"
      :aria-label="`${section.label}, ${section.remainingText} remaining${section.current ? ', current section' : ''}`"
    >
      <div class="timeline-caption">
        <span class="timeline-name">{{ section.label }}</span>
        <span class="timeline-time">{{ section.remainingText }}</span>
      </div>
      <div class="timeline-track"><div class="timeline-progress" :style="{ width: `${section.progress}%` }"></div></div>
    </div>
  </nav>
</template>

<style scoped>
:global(.slidev-layout) {
  box-sizing: border-box;
  padding-bottom: 64px !important;
}
:global(.slidev-layout .absolute.inset-0) {
  padding-bottom: 64px !important;
}
.workshop-timer {
  position: fixed;
  z-index: 1000;
  top: 7px;
  right: 10px;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 5px 8px;
  border: 1px solid #cbd5e1;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.96);
  color: #1e2530;
  box-shadow: 0 2px 8px #0003;
  font: 9px 'JetBrains Mono', monospace;
  line-height: 1;
  white-space: nowrap;
}
.timer-gauge { width: 56px; height: 56px; flex: none; }
.gauge-total, .gauge-slide {
  display: grid;
  place-items: center;
  border-radius: 50%;
  background: conic-gradient(var(--ring-color, #64748b) 0 var(--progress), #e2e8f0 var(--progress) 100%);
  transition: background 220ms linear;
}
.gauge-total { width: 56px; height: 56px; }
.gauge-slide { width: 39px; height: 39px; background: conic-gradient(var(--ring-color, #64748b) 0 var(--progress), #cbd5e1 var(--progress) 100%); }
.gauge-slide strong {
  display: grid;
  place-items: center;
  width: 31px;
  height: 31px;
  border-radius: 50%;
  background: #fff;
  color: #1e2530;
  font-size: 8px;
  font-variant-numeric: tabular-nums;
}
.timer-readout { display: grid; gap: 5px; }
.clock-group { display: flex; align-items: center; gap: 6px; }
.clock-label { color: #64748b; letter-spacing: .04em; }
.clock-group strong { color: #1e2530; font-size: 11px; font-variant-numeric: tabular-nums; }
.clock-group strong.overtime { color: #b91c1c; }
.warning-yellow { --ring-color: #eab308; }
.warning-orange { --ring-color: #D9772B; }
.warning-red { --ring-color: #dc2626; }
.workshop-timer.warning-yellow { border-color: #eab308; background: #fefce8; }
.workshop-timer.warning-orange { border-color: #D9772B; background: #fff7ed; }
.workshop-timer.warning-red { border-color: #dc2626; background: #fff1f2; }
.workshop-timer.warning-yellow .clock-group strong { color: #a16207; }
.workshop-timer.warning-orange .clock-group strong { color: #c2410c; }
.workshop-timer.warning-red .clock-label, .workshop-timer.warning-red .overdue-label { color: #b91c1c; }
.overdue-label { font-weight: 700; }
.timer-reset {
  cursor: pointer;
  border: 1px solid #cbd5e1;
  border-radius: 999px;
  padding: 3px 6px;
  background: #f1f5f9;
  color: #1e2530;
  font: 11px 'JetBrains Mono', monospace;
}
.timer-reset { padding-inline: 5px; }
.timer-reset:hover { border-color: #64748b; }
@media print { .workshop-timer { display: none; } }
.workshop-timeline {
  position: fixed;
  z-index: 999;
  right: 12px;
  bottom: 7px;
  left: 12px;
  display: flex;
  align-items: stretch;
  gap: 5px;
  padding: 5px 7px 4px;
  border: 1px solid #dbe1e8;
  border-radius: 9px;
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 1px 6px #0002;
  color: #475569;
  pointer-events: none;
}
.timeline-section {
  min-width: 0;
  flex-basis: 0;
  opacity: 0.68;
}
.timeline-section.current { opacity: 1; }
.timeline-caption {
  display: flex;
  justify-content: space-between;
  gap: 3px;
  margin-bottom: 3px;
  white-space: nowrap;
  font: 6px/1.2 'JetBrains Mono', monospace;
  font-variant-numeric: tabular-nums;
}
.timeline-name { overflow: hidden; text-overflow: ellipsis; }
.timeline-time { flex: none; }
.timeline-track {
  height: 3px;
  overflow: hidden;
  border-radius: 99px;
  background: #e2e8f0;
}
.timeline-progress {
  height: 100%;
  border-radius: inherit;
  background: #64748b;
  transition: width 220ms linear;
}
.timeline-section.current .timeline-progress { background: #334155; }
.timeline-section.overdue .timeline-time { color: #b91c1c; font-weight: 700; }
.timeline-section.overdue .timeline-progress { background: #dc2626; }
@media print { .workshop-timeline { display: none; } }
</style>
