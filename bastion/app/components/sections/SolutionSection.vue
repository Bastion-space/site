<template>
  <section
    id="solution"
    class="scroll-mt-20 px-4 py-20 sm:px-6 sm:py-24 lg:px-8"
  >
    <div class="mx-auto max-w-6xl">
      <div class="text-center">
        <span class="text-sm font-semibold uppercase tracking-wider text-slate-500">
          The Solution
        </span>
      </div>

      <div class="mt-8 text-center">
        <h1 class="text-8xl font-black tracking-tighter text-white sm:text-9xl md:text-[10rem]">
          DAEMON
        </h1>
        <div class="mt-4 flex justify-center gap-4">
          <span class="rounded-full bg-red-900/40 px-6 py-2 text-sm font-semibold uppercase tracking-wider text-red-300">
            Active RF Defense
          </span>
          <span class="rounded-full bg-slate-800 px-6 py-2 text-sm font-semibold uppercase tracking-wider text-slate-300">
            Defense Grade
          </span>
        </div>
      </div>

      <p class="mx-auto mt-12 max-w-4xl text-center text-xl text-slate-300 sm:text-2xl">
        Space-qualified RF subsystem protecting sovereign assets<br />
        in contested environments through active defense.
      </p>

      <div ref="statsRef" class="mt-16 grid gap-4 sm:grid-cols-3">
        <div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6 text-center">
          <div class="text-4xl font-bold text-white">{{ animated.modes }}</div>
          <div class="mt-2 text-sm uppercase tracking-wider text-slate-400">Modes</div>
          <p class="mt-1 text-xs text-slate-500">Detect · Localize · Counter</p>
        </div>
        <div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6 text-center">
          <div class="text-4xl font-bold text-white">{{ animated.awareness }}°</div>
          <div class="mt-2 text-sm uppercase tracking-wider text-slate-400">Awareness</div>
          <p class="mt-1 text-xs text-slate-500">Full RF spectrum surveillance</p>
        </div>
        <div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6 text-center">
          <div class="text-4xl font-bold text-white">{{ animated.latency }}s</div>
          <div class="mt-2 text-sm uppercase tracking-wider text-slate-400">Latency</div>
          <p class="mt-1 text-xs text-slate-500">Real-time countermeasures</p>
        </div>
      </div>

      <p class="mt-16 text-center text-sm text-slate-500">
        Built for sovereignty. Operates under attack.
      </p>
    </div>
  </section>
</template>

<script setup lang="ts">
const statsRef = ref<HTMLElement | null>(null)

const animated = reactive({
  modes: 0,
  awareness: 0,
  latency: 0,
})

function animateValue(key: keyof typeof animated, target: number, duration: number) {
  const start = performance.now()
  const update = (now: number) => {
    const progress = Math.min((now - start) / duration, 1)
    const eased = 1 - Math.pow(1 - progress, 3)
    animated[key] = Math.round(eased * target)
    if (progress < 1) requestAnimationFrame(update)
  }
  requestAnimationFrame(update)
}

let triggered = false

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting && !triggered) {
        triggered = true
        animateValue('modes', 3, 800)
        animateValue('awareness', 360, 1500)
        animateValue('latency', 2, 600)
        observer.disconnect()
      }
    },
    { threshold: 0.4 }
  )
  if (statsRef.value) observer.observe(statsRef.value)
})
</script>

<style scoped>
h1 {
  text-shadow: 0 0 30px rgba(239, 68, 68, 0.3);
  background: linear-gradient(90deg,
    #000091 0%,
    #000091 20%,
    #fff 60%,
    #e1000f 80%,
    #e1000f 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
</style>
