<template>
  <section
    id="business"
    ref="sectionRef"
    class="scroll-mt-20 relative px-4 py-20 sm:px-6 sm:py-24 lg:px-8 overflow-hidden"
    @mousemove="handleMouseMove"
    @mouseleave="handleMouseLeave"
  >
    <!-- Fond interactif (dégradé radial qui suit la souris) -->
    <div
      class="absolute inset-0 bg-gradient-to-b from-slate-900/80 to-transparent"
      :style="{
        backgroundImage: `radial-gradient(ellipse at ${mouseX}% ${mouseY}%, rgba(59,130,246,0.12) 0%, transparent 70%)`
      }"
    ></div>

    <!-- Étoiles de fond -->
    <div class="absolute inset-0 stars"></div>

    <!-- Contenu principal -->
    <div class="relative mx-auto max-w-6xl z-10">
      <!-- En‑tête -->
      <div class="text-center mb-16">
        <h2 class="text-5xl font-bold tracking-tight text-white sm:text-6xl md:text-7xl">
          Demonstration
        </h2>
        <div class="mx-auto mt-4 h-1 w-24 bg-gradient-to-r from-blue-400 via-white to-blue-400"></div>
        <p class="mt-6 text-xl text-slate-400 max-w-2xl mx-auto">
          See how our anti‑jamming protection detects and neutralises interference.
        </p>
      </div>

      <!-- Zone de démonstration – fond totalement transparent -->
      <div class="relative w-full rounded-2xl border border-slate-800/10 p-4">
        <div class="relative aspect-video w-full overflow-hidden rounded-xl">

        <!-- TERRE -->
        <svg class="absolute inset-0 h-full w-full pointer-events-none" viewBox="0 0 800 450">
        <defs>
          <radialGradient id="oceanGrad" cx="55%" cy="65%" r="65%">
            <stop offset="0%" stop-color="#1a4a7a" />
            <stop offset="35%" stop-color="#1e5a8a" />
            <stop offset="70%" stop-color="#163a5e" />
            <stop offset="100%" stop-color="#0d1f33" />
          </radialGradient>
          <linearGradient id="landGrad" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stop-color="#4a9a5a" />
            <stop offset="100%" stop-color="#2d7a4f" />
          </linearGradient>
          <filter id="continentShadow">
            <feDropShadow dx="0" dy="0" stdDeviation="2" flood-color="rgba(0,0,0,0.3)" />
          </filter>
        </defs>

        <circle cx="180" cy="420" r="160" fill="url(#oceanGrad)" opacity="0.7" />
        <circle cx="180" cy="420" r="162" fill="none" stroke="rgba(80,180,255,0.15)" stroke-width="6" />
        <circle cx="180" cy="420" r="170" fill="none" stroke="rgba(80,180,255,0.08)" stroke-width="10" />
        <circle cx="180" cy="420" r="180" fill="none" stroke="rgba(80,180,255,0.04)" stroke-width="15" />

        <g fill="url(#landGrad)" opacity="0.7" stroke="#5aaa6a" stroke-width="0.8">
          <path
            d="M 30 340 
              Q 40 320 60 305 
              Q 80 295 100 292 
              Q 120 290 140 295 
              Q 160 305 165 320 
              Q 170 340 160 360 
              Q 150 380 130 390 
              Q 110 400 90 395 
              Q 70 388 55 375 
              Q 40 360 30 340 Z"
          />
        </g>

        <g fill="rgba(255,220,100,0.6)">
          <circle cx="145" cy="330" r="1.5" />
          <circle cx="105" cy="290" r="1" />
          <circle cx="195" cy="300" r="1.5" />
          <circle cx="90" cy="390" r="1" />
        </g>
      </svg>

          <!-- ===== STATION SOL / SATELLITE / JAMMER (mêmes coordonnées que les ondes ci-dessous) ===== -->
          <svg class="absolute inset-0 h-full w-full pointer-events-none" viewBox="0 0 800 450">
            <!-- Ground Station : ancrée exactement au point d'origine de l'onde (70,250) -->
            <g>
              <ellipse cx="70" cy="254" rx="11" ry="5" fill="#cbd5e1" />
              <circle cx="70" cy="250" r="3" fill="#4ade80" />
              <line x1="70" y1="257" x2="70" y2="290" stroke="#94a3b8" stroke-width="2.5" stroke-linecap="round" vector-effect="non-scaling-stroke" />
              <rect x="62" y="290" width="16" height="10" fill="rgba(51,65,85,0.85)" stroke="#475569" stroke-width="0.7" vector-effect="non-scaling-stroke" />
              <rect x="54" y="302" width="32" height="2" fill="rgba(30,41,59,0.5)" />
            </g>

            <!-- Friendly Satellite : ancré exactement au point d'arrivée de l'onde (400,120) -->
            <g>
              <rect x="369" y="113" width="13" height="13" rx="1.5" fill="rgba(147,197,253,0.8)" />
              <rect x="419" y="113" width="13" height="13" rx="1.5" fill="rgba(147,197,253,0.8)" />
              <circle cx="400" cy="120" r="16" fill="#e2e8f0" />
              <line x1="400" y1="104" x2="400" y2="94" stroke="#94a3b8" stroke-width="2" vector-effect="non-scaling-stroke" />
              <circle cx="400" cy="91" r="2.6" fill="#ef4444">
                <animate attributeName="opacity" values="1;0.5;1" dur="2s" repeatCount="indefinite" />
              </circle>
              <circle v-if="isProtected" cx="400" cy="120" r="42" fill="none" stroke="#22d3ee" stroke-width="4" opacity="0.9" vector-effect="non-scaling-stroke">
                <animate attributeName="opacity" values="0.9;0.4;0.9" dur="2s" repeatCount="indefinite" />
              </circle>
              <circle v-if="jamming && !isProtected" cx="400" cy="120" r="20" fill="none" stroke="rgba(239,68,68,0.6)" stroke-width="4" vector-effect="non-scaling-stroke">
                <animate attributeName="r" values="20;38" dur="1.5s" repeatCount="indefinite" />
                <animate attributeName="opacity" values="0.6;0" dur="1.5s" repeatCount="indefinite" />
              </circle>
            </g>

            <!-- Jammer : ancré exactement au point d'origine de l'onde de brouillage (740,130) -->
            <g>
              <circle cx="740" cy="130" r="13" fill="rgba(127,29,29,0.85)" stroke="#b91c1c" stroke-width="1.3" vector-effect="non-scaling-stroke" />
              <text x="740" y="134.5" text-anchor="middle" font-size="12" font-weight="700" fill="#fca5a5" font-family="system-ui, sans-serif">J</text>
              <line x1="740" y1="117" x2="740" y2="106" stroke="#ef4444" stroke-width="2" vector-effect="non-scaling-stroke" />
              <circle cx="740" cy="103" r="2.3" fill="#f87171">
                <animate attributeName="opacity" values="1;0.5;1" dur="2s" repeatCount="indefinite" />
              </circle>
            </g>
          </svg>

          <!-- ===== LIBELLÉS (HTML, taille indépendante de l'échelle du SVG pour rester lisibles sur mobile) ===== -->
          <span class="pointer-events-none absolute top-[70%] left-[8.75%] -translate-x-1/2 whitespace-nowrap text-xs font-semibold text-blue-300 sm:text-sm">
            Ground Station
          </span>
          <span class="pointer-events-none absolute top-[38%] left-1/2 -translate-x-1/2 whitespace-nowrap text-xs font-semibold text-white sm:text-sm">
            Friendly Satellite
          </span>
          <span class="pointer-events-none absolute top-[33%] left-[92.5%] -translate-x-1/2 whitespace-nowrap text-xs font-semibold text-red-400 sm:text-sm">
            Jammer
          </span>


          <!-- ===== SIGNAL LÉGITIME ===== -->
          <svg class="absolute inset-0 h-full w-full pointer-events-none" viewBox="0 0 800 450">
            <g v-if="!(jamming && !isProtected)">
              <path
                :d="sineWaveVariable(70, 250, 400, 120, 5, 40, 15, 0)"
                fill="none"
                :stroke="signalColor"
                stroke-width="2.5"
                stroke-linecap="round"
              >
                <animate attributeName="stroke-dashoffset" from="0" to="-80" dur="1.2s" repeatCount="indefinite" />
              </path>
              <path
                :d="sineWaveVariable(70, 250, 400, 120, 5, 40, 15, 4)"
                fill="none"
                :stroke="signalColorSecondary"
                stroke-width="2"
                stroke-linecap="round"
                opacity="0.4"
              >
                <animate attributeName="stroke-dashoffset" from="0" to="-80" dur="1.2s" repeatCount="indefinite" />
              </path>
            </g>

            <g v-if="jamming">
              <path
                :d="jammingPath"
                fill="none"
                stroke="#ef4444"
                stroke-width="2.5"
                stroke-linecap="round"
                opacity="0.9"
              >
                <animate attributeName="stroke-dashoffset" from="0" to="-60" dur="0.8s" repeatCount="indefinite" />
              </path>
              <path
                :d="jammingPathSecondary"
                fill="none"
                stroke="#dc2626"
                stroke-width="2"
                stroke-linecap="round"
                opacity="0.5"
              >
                <animate attributeName="stroke-dashoffset" from="0" to="-60" dur="0.8s" repeatCount="indefinite" />
              </path>
            </g>
          </svg>

          <!-- ===== SIGNAL ERRATIQUE ===== -->
          <div v-if="jamming && !isProtected" class="absolute inset-0 pointer-events-none">
            <svg class="h-full w-full" viewBox="0 0 800 450">
              <g fill="none" stroke="#f87171" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                <polyline :points="erraticPulse(87, 244, 98, 238, 12, 0.1)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.15s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(113, 230, 124, 224, 18, 0.3)">
                  <animate attributeName="opacity" values="0.8;0;0.8" dur="0.12s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(139, 216, 150, 210, 14, 0.5)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.18s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(166, 202, 177, 196, 22, 0.05)">
                  <animate attributeName="opacity" values="0.7;0;0.7" dur="0.1s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(192, 188, 203, 182, 16, 0.6)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.14s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(218, 174, 229, 168, 25, 0.2)">
                  <animate attributeName="opacity" values="0.8;0;0.8" dur="0.09s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(244, 160, 255, 154, 19, 0.4)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.2s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(270, 146, 281, 140, 23, 0.15)">
                  <animate attributeName="opacity" values="0.7;0;0.7" dur="0.11s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(296, 132, 307, 126, 17, 0.45)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.16s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(322, 118, 333, 112, 26, 0.25)">
                  <animate attributeName="opacity" values="0.8;0;0.8" dur="0.13s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(348, 104, 359, 98, 20, 0.5)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.17s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(374, 90, 385, 84, 14, 0.1)">
                  <animate attributeName="opacity" values="0.9;0;0.9" dur="0.12s" repeatCount="indefinite" />
                </polyline>
                <polyline :points="erraticPulse(395, 120, 406, 118, 10, 0.3)">
                  <animate attributeName="opacity" values="0.8;0;0.8" dur="0.08s" repeatCount="indefinite" />
                </polyline>
              </g>

              <g fill="#fbbf24">
                <circle cx="100" cy="240" r="3">
                  <animate attributeName="opacity" values="1;0;1" dur="0.2s" repeatCount="indefinite" />
                </circle>
                <circle cx="145" cy="220" r="4">
                  <animate attributeName="opacity" values="1;0;1" dur="0.15s" repeatCount="indefinite" />
                </circle>
                <circle cx="200" cy="190" r="3.5">
                  <animate attributeName="opacity" values="1;0;1" dur="0.25s" repeatCount="indefinite" />
                </circle>
                <circle cx="265" cy="155" r="3">
                  <animate attributeName="opacity" values="1;0;1" dur="0.18s" repeatCount="indefinite" />
                </circle>
                <circle cx="330" cy="120" r="4">
                  <animate attributeName="opacity" values="1;0;1" dur="0.12s" repeatCount="indefinite" />
                </circle>
                <circle cx="385" cy="95" r="3.5">
                  <animate attributeName="opacity" values="1;0;1" dur="0.22s" repeatCount="indefinite" />
                </circle>
              </g>

              <g stroke="#fca5a5" stroke-width="1.5" stroke-linecap="round" opacity="0.6">
                <line x1="92" y1="242" x2="97" y2="237">
                  <animate attributeName="opacity" values="0.6;0;0.6" dur="0.1s" repeatCount="indefinite" />
                </line>
                <line x1="125" y1="228" x2="130" y2="223">
                  <animate attributeName="opacity" values="0.5;0;0.5" dur="0.13s" repeatCount="indefinite" />
                </line>
                <line x1="175" y1="205" x2="180" y2="200">
                  <animate attributeName="opacity" values="0.7;0;0.7" dur="0.09s" repeatCount="indefinite" />
                </line>
                <line x1="235" y1="172" x2="240" y2="167">
                  <animate attributeName="opacity" values="0.4;0;0.4" dur="0.14s" repeatCount="indefinite" />
                </line>
                <line x1="295" y1="140" x2="300" y2="135">
                  <animate attributeName="opacity" values="0.6;0;0.6" dur="0.11s" repeatCount="indefinite" />
                </line>
                <line x1="370" y1="100" x2="375" y2="95">
                  <animate attributeName="opacity" values="0.5;0;0.5" dur="0.12s" repeatCount="indefinite" />
                </line>
              </g>
            </svg>
          </div>

          <!-- ===== MESSAGES ===== -->
          <div
            v-if="detected"
            class="absolute left-1/2 top-[2%] w-[92%] max-w-md -translate-x-1/2 whitespace-nowrap rounded-full px-2 py-1 text-center text-[10px] font-semibold text-red-400 border border-red-500/20 sm:w-auto sm:px-4 sm:py-2 sm:text-base"
          >
            ⚡ JAMMING DETECTED – PROTECTION ACTIVE
          </div>

          <div
            v-if="isProtected && jamming"
            class="absolute left-1/2 top-[38%] -translate-x-1/2 whitespace-nowrap text-[10px] font-medium text-cyan-400 px-2 py-1 rounded-full border border-cyan-500/20 sm:px-3 sm:text-sm"
          >
            🛡️ Jamming absorbed
          </div>

          <!-- ===== STATUS ===== -->
          <div class="absolute bottom-[3%] left-1/2 -translate-x-1/2 text-center">
            <p class="text-xs text-slate-400 sm:text-base">
              Status:
              <span v-if="!jamming" class="text-green-400">🟢 Secure</span>
              <span v-else-if="jamming && !isProtected" class="text-red-400">🔴 Jamming</span>
              <span v-else-if="jamming && isProtected" class="text-cyan-400">🛡️ Protected</span>
            </p>
          </div>

        </div><!-- fin zone visuelle -->

        <!-- ===== CONTRÔLES ===== -->
        <div class="mt-6 flex flex-wrap items-center justify-center gap-4">
          <button
            @click="toggleJamming"
            class="inline-flex items-center gap-2 rounded-lg px-6 py-3 text-base font-medium transition hover:scale-105"
            :class="jamming ? 'bg-red-600 hover:bg-red-500 text-white' : 'bg-blue-600 hover:bg-blue-500 text-white'"
          >
            <span v-if="!jamming">▶ Activate Jamming</span>
            <span v-else>⏹ Stop Jamming</span>
          </button>
          <button
            @click="resetDemo"
            class="rounded-lg border border-slate-600 px-6 py-3 text-base font-medium text-slate-300 transition hover:border-slate-400 hover:bg-slate-800/50"
          >
            Reset
          </button>
        </div>

        <!-- ===== LÉGENDE ===== -->
        <div class="mt-4 flex flex-wrap justify-center gap-6 text-sm text-slate-500">
          <span class="flex items-center gap-1">
            <span class="inline-block h-3 w-3 rounded-full bg-green-400"></span>
            Legitimate Signal
          </span>
          <span class="flex items-center gap-1">
            <span class="inline-block h-3 w-3 rounded-full bg-red-500"></span>
            Jamming Emission
          </span>
          <span class="flex items-center gap-1">
            <span class="inline-block h-3 w-3 rounded-full border-2 border-cyan-400 bg-transparent"></span>
            Bastion Space Shield
          </span>
          <span class="flex items-center gap-1">
            <span class="inline-block h-3 w-3 rounded-full bg-yellow-400"></span>
            RF Interference
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed, onBeforeUnmount } from 'vue'

// --- État ---
const jamming = ref(false)
const isProtected = ref(false)
const detected = ref(false)
let timeoutId: number | null = null

// --- Fond interactif ---
const sectionRef = ref<HTMLElement | null>(null)
const mouseX = ref(50)
const mouseY = ref(50)

function handleMouseMove(event: MouseEvent) {
  if (!sectionRef.value) return
  const rect = sectionRef.value.getBoundingClientRect()
  const x = ((event.clientX - rect.left) / rect.width) * 100
  const y = ((event.clientY - rect.top) / rect.height) * 100
  mouseX.value = Math.min(100, Math.max(0, x))
  mouseY.value = Math.min(100, Math.max(0, y))
}

function handleMouseLeave() {
  mouseX.value = 50
  mouseY.value = 50
}

// --- Couleurs du signal ---
const signalColor = computed(() => {
  if (jamming.value && !isProtected.value) return '#f87171'
  return '#4ade80'
})

const signalColorSecondary = computed(() => {
  if (jamming.value && !isProtected.value) return '#dc2626'
  return '#22c55e'
})

// --- Fonctions ---
function sineWaveVariable(
  x1: number,
  y1: number,
  x2: number,
  y2: number,
  amplitudeMin: number,
  amplitudeMax: number,
  wavelength: number,
  phase: number = 0
): string {
  const steps = 60
  let path = `M ${x1} ${y1}`
  
  const dx = x2 - x1
  const dy = y2 - y1
  const length = Math.sqrt(dx * dx + dy * dy)
  if (length === 0) return path + ` L ${x2} ${y2}`
  
  const nx = -dy / length
  const ny = dx / length
  
  for (let i = 0; i <= steps; i++) {
    const t = i / steps
    const px = x1 + t * dx
    const py = y1 + t * dy
    const amplitude = amplitudeMin + (amplitudeMax - amplitudeMin) * (t * t * 0.8 + t * 0.2)
    const angle = (i / steps) * 2 * Math.PI * (steps / wavelength) + phase
    const offset = amplitude * Math.sin(angle)
    const ox = px + nx * offset
    const oy = py + ny * offset
    path += ` L ${ox.toFixed(2)} ${oy.toFixed(2)}`
  }
  
  return path
}

function sineWavePartial(
  x1: number,
  y1: number,
  x2: number,
  y2: number,
  amplitudeMin: number,
  amplitudeMax: number,
  wavelength: number,
  phase: number = 0,
  fraction: number = 1
): string {
  const steps = 60
  const maxSteps = Math.floor(steps * fraction)
  let path = `M ${x1} ${y1}`
  
  const dx = x2 - x1
  const dy = y2 - y1
  const length = Math.sqrt(dx * dx + dy * dy)
  if (length === 0) return path + ` L ${x2} ${y2}`
  
  const nx = -dy / length
  const ny = dx / length
  
  for (let i = 0; i <= maxSteps; i++) {
    const t = i / steps
    const px = x1 + t * dx
    const py = y1 + t * dy
    const amplitude = amplitudeMin + (amplitudeMax - amplitudeMin) * (t * t * 0.8 + t * 0.2)
    const angle = (i / steps) * 2 * Math.PI * (steps / wavelength) + phase
    const offset = amplitude * Math.sin(angle)
    const ox = px + nx * offset
    const oy = py + ny * offset
    path += ` L ${ox.toFixed(2)} ${oy.toFixed(2)}`
  }
  
  return path
}

function erraticPulse(
  x1: number,
  y1: number,
  x2: number,
  y2: number,
  amplitude: number,
  offset: number
): string {
  const midX = (x1 + x2) / 2 + (Math.random() - 0.5) * 30
  const midY = (y1 + y2) / 2 - amplitude + (Math.random() - 0.5) * 20
  return `${x1},${y1} ${midX},${midY} ${x2},${y2}`
}

// --- Chemins du signal de brouillage ---
const jammingPath = computed(() => {
  if (isProtected.value) {
    return sineWavePartial(740, 130, 400, 120, 5, 30, 12, 0, 0.80)
  } else {
    return sineWaveVariable(740, 130, 400, 120, 5, 30, 12, 0)
  }
})

const jammingPathSecondary = computed(() => {
  if (isProtected.value) {
    return sineWavePartial(740, 130, 400, 120, 5, 30, 12, 3, 0.80)
  } else {
    return sineWaveVariable(740, 130, 400, 120, 5, 30, 12, 3)
  }
})

// --- Méthodes ---
function toggleJamming() {
  if (jamming.value) {
    jamming.value = false
    isProtected.value = false
    detected.value = false
    if (timeoutId) {
      clearTimeout(timeoutId)
      timeoutId = null
    }
  } else {
    jamming.value = true
    isProtected.value = false
    detected.value = false
    timeoutId = setTimeout(() => {
      if (jamming.value) {
        isProtected.value = true
        detected.value = true
      }
      timeoutId = null
    }, 2000)
  }
}

function resetDemo() {
  if (timeoutId) {
    clearTimeout(timeoutId)
    timeoutId = null
  }
  jamming.value = false
  isProtected.value = false
  detected.value = false
}

onBeforeUnmount(() => {
  if (timeoutId) {
    clearTimeout(timeoutId)
  }
})
</script>

<style scoped>
.stars {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(2px 2px at 20px 30px, #eee, transparent),
                    radial-gradient(2px 2px at 40px 70px, rgba(255,255,255,0.8), transparent),
                    radial-gradient(1px 1px at 90px 40px, #fff, transparent),
                    radial-gradient(1px 1px at 130px 80px, rgba(255,255,255,0.6), transparent),
                    radial-gradient(2px 2px at 160px 30px, #ddd, transparent);
  background-size: 200px 100px;
  background-repeat: repeat;
  opacity: 0.4;
  pointer-events: none;
}

@keyframes ping {
  75%, 100% {
    transform: scale(2);
    opacity: 0;
  }
}
.animate-ping {
  animation: ping 1.5s cubic-bezier(0, 0, 0.2, 1) infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}
.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

path {
  stroke-dasharray: 30 50;
  stroke-dashoffset: 0;
}
</style>