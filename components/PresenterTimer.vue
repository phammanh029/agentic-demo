<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

type Status = 'idle' | 'running' | 'paused'
type TimerState = { status: Status; section: number; overallBase: number; sectionBase: number; resumedAt: number | null }

const sections = [
  { name: 'Introduction and task', seconds: 5 * 60 },
  { name: 'Prompt-driven demo', seconds: 15 * 60 },
  { name: 'Agentic demo', seconds: 15 * 60 },
  { name: 'Compare results and trade-offs', seconds: 15 * 60 },
  { name: 'Discussion and next steps', seconds: 10 * 60 },
]
const storageKey = 'shop6-agentic-workshop-timer-v1'
const state = ref<TimerState>(load())
const now = ref(Date.now())
let heartbeat: number | undefined

function load(): TimerState {
  try {
    const saved = JSON.parse(localStorage.getItem(storageKey) || '')
    if (saved && typeof saved.section === 'number') return saved
  } catch { /* first run or malformed local state */ }
  return { status: 'idle', section: 0, overallBase: 0, sectionBase: 0, resumedAt: null }
}
function persist() { localStorage.setItem(storageKey, JSON.stringify(state.value)) }
function elapsed(base: number, resumedAt: number | null) { return state.value.status === 'running' && resumedAt ? base + now.value - resumedAt : base }
const overallMs = computed(() => elapsed(state.value.overallBase, state.value.resumedAt))
const sectionMs = computed(() => elapsed(state.value.sectionBase, state.value.resumedAt))
const section = computed(() => sections[state.value.section])
const nextTopic = computed(() => sections[state.value.section + 1])
const sectionRemaining = computed(() => section.value.seconds * 1000 - sectionMs.value)
const overallRemaining = computed(() => 60 * 60 * 1000 - overallMs.value)
const expired = computed(() => sectionRemaining.value <= 0)
const overallExpired = computed(() => overallRemaining.value <= 0)
const wrapUp = computed(() => sectionRemaining.value <= 120000 && sectionRemaining.value > 30000)
const finalCue = computed(() => sectionRemaining.value <= 30000 && sectionRemaining.value > 0)
const visibleOvertime = computed(() => Math.max(0, -sectionRemaining.value))
const overallText = computed(() => format(overallRemaining.value))
const sectionText = computed(() => expired.value ? `+${format(visibleOvertime.value)}` : format(sectionRemaining.value))
function format(ms: number) { const total = Math.floor(Math.abs(ms) / 1000); return `${String(Math.floor(total / 60)).padStart(2, '0')}:${String(total % 60).padStart(2, '0')}` }
function commit() {
  if (state.value.status !== 'running' || !state.value.resumedAt) return
  state.value.overallBase += now.value - state.value.resumedAt
  state.value.sectionBase += now.value - state.value.resumedAt
  state.value.resumedAt = null
}
function start() { if (state.value.status === 'idle' || state.value.status === 'paused') { state.value.status = 'running'; state.value.resumedAt = Date.now(); persist() } }
function pause() { commit(); state.value.status = 'paused'; persist() }
function nextSection() {
  commit();
  if (state.value.section < sections.length - 1) state.value.section += 1
  state.value.sectionBase = 0
  if (state.value.status === 'running') state.value.resumedAt = Date.now()
  persist()
}
function reset() {
  if (state.value.status !== 'idle' && !window.confirm('Reset the active workshop timer?')) return
  state.value = { status: 'idle', section: 0, overallBase: 0, sectionBase: 0, resumedAt: null }
  persist()
}
onMounted(() => { heartbeat = window.setInterval(() => { now.value = Date.now() }, 250) })
onBeforeUnmount(() => { if (heartbeat) window.clearInterval(heartbeat) })
</script>

<template>
  <aside class="presenter-timer" :class="{ 'is-expired': expired, 'is-wrap': wrapUp, 'is-final': finalCue }" aria-label="Workshop presenter timer">
    <div class="timer-header"><span class="timer-title">WORKSHOP TIMER · PRESENTER ONLY</span><span class="timer-status">{{ state.status }}</span></div>
    <div class="timer-main"><div><small>SECTION {{ state.section + 1 }}/5</small><strong>{{ sectionText }}</strong><span>{{ section.name }}</span><em v-if="nextTopic">NEXT: {{ nextTopic.name }}</em><em v-else>NEXT: close and discuss</em></div><div class="overall"><small>OVERALL REMAINING</small><strong>{{ overallText }}</strong><span v-if="overallExpired">overall overtime</span><span v-else>60-minute session</span></div></div>
    <div class="timer-progress"><i :style="{ width: `${Math.min(100, Math.max(0, sectionMs / (section.seconds * 1000) * 100))}%` }"></i></div>
    <div v-if="expired" class="timer-cue">MOVE TO NEXT SECTION · demo can continue</div><div v-else-if="finalCue" class="timer-cue">30 SECONDS · stronger wrap cue</div><div v-else-if="wrapUp" class="timer-cue">2 MINUTES · wrap up</div><div v-else class="timer-cue muted-cue">Timing is independent of slide navigation</div>
    <div class="timer-controls"><button v-if="state.status !== 'running'" @click="start">{{ state.status === 'paused' ? 'Resume' : 'Start' }}</button><button v-else @click="pause">Pause</button><button @click="nextSection" :disabled="state.section === sections.length - 1">Next section</button><button class="reset" @click="reset">Reset</button></div>
    <div class="timer-help">Pause freezes both clocks · expiry shows overtime and never auto-advances · refresh-safe</div>
  </aside>
</template>

<style scoped>
.presenter-timer{position:fixed;right:18px;bottom:18px;width:370px;padding:14px 16px;border:1px solid #425a77;border-radius:14px;background:rgba(7,15,27,.97);box-shadow:0 18px 45px #0008;color:#eef6ff;font:12px Inter,sans-serif;z-index:1000}.timer-header,.timer-main,.timer-controls{display:flex;justify-content:space-between;align-items:center;gap:10px}.timer-title,.timer-status,small,.timer-help{font:10px 'JetBrains Mono',monospace;letter-spacing:.08em;color:#9db1c9}.timer-status{color:#4de1d2}.timer-main{margin:10px 0}.timer-main div:first-child{display:grid;gap:3px}.timer-main strong{font:700 30px 'JetBrains Mono';color:#4de1d2}.timer-main span{color:#c4d1e0}.timer-main em{color:#a78bfa;font:600 10px 'JetBrains Mono';font-style:normal}.overall{text-align:right;display:grid;gap:3px}.overall strong{font:700 18px 'JetBrains Mono';color:#fff}.timer-progress{height:5px;border-radius:10px;background:#24374f;overflow:hidden}.timer-progress i{display:block;height:100%;background:#4de1d2;transition:width .2s linear}.timer-cue{margin:10px 0;color:#f6c453;font:700 11px 'JetBrains Mono';letter-spacing:.04em}.muted-cue{color:#8194ac;font-weight:400}.timer-controls{justify-content:flex-start}.timer-controls button{cursor:pointer;border:1px solid #4d6887;border-radius:7px;padding:6px 9px;background:#13263b;color:#eaf3fc;font:600 11px Inter}.timer-controls button:hover{border-color:#4de1d2}.timer-controls button:disabled{opacity:.4;cursor:not-allowed}.timer-controls .reset{margin-left:auto;color:#ff9da8;border-color:#6e3c4b}.timer-help{margin-top:10px;font-size:9px;letter-spacing:0}.is-expired{border-color:#f6c453}.is-expired .timer-main strong{color:#f6c453}.is-final{border-color:#ff7b8b}.is-final .timer-main strong{color:#ff7b8b}.is-final .timer-progress i{background:#ff7b8b}.is-wrap .timer-progress i{background:#f6c453}
</style>
