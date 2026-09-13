<template>
  <section
    id="solution"
    class="scroll-mt-20 px-4 py-20 sm:px-6 sm:py-24 lg:px-8"
  >
    <div class="mx-auto max-w-6xl">

      <!-- === En-tête === -->
      <div class="text-center">
        <span class="text-sm font-semibold uppercase tracking-wider text-slate-400 sm:text-base">
          The Solution
        </span>
        <h1 class="mt-6 text-3xl font-black leading-tight tracking-tight text-white sm:text-5xl md:text-6xl">
          BASTION SPACE
        </h1>
        <div class="mt-4 flex flex-wrap justify-center gap-2 sm:gap-4">
          <span class="rounded-full bg-red-900/40 px-4 py-1.5 text-sm font-semibold uppercase tracking-wider text-red-300 sm:px-6 sm:py-2">
            Continuous RF Defense
          </span>

          <a
            href="https://www.bordeaux-inp.fr/fr/lincubateur-bordeaux-inpulse"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-2 rounded-full border border-slate-700 bg-slate-800/50 px-4 py-1.5 text-sm font-semibold uppercase tracking-wider text-slate-300 transition hover:border-blue-500/50 hover:bg-slate-800 hover:text-blue-300 sm:px-6 sm:py-2"
          >
            Incubated Solution
          </a>
        </div>

        <p class="mx-auto mt-8 max-w-3xl text-lg text-slate-200 sm:mt-12 sm:text-xl">
          Space RF subsystem protecting sovereign assets in contested environments.
        </p>
      </div>

      <!-- === Le problème === -->
      <div class="mt-16 grid gap-6 md:grid-cols-2 md:gap-10">
        <div class="rounded-2xl border border-red-900/30 bg-red-950/10 p-6 sm:p-8">
          <div class="mb-3 inline-flex items-center gap-2 text-sm font-semibold uppercase tracking-wider text-red-400">
            <span class="inline-block size-2 rounded-full bg-red-500"></span>
            The threat
          </div>
          <h3 class="text-xl font-bold text-white sm:text-2xl">
            Contested spectrum
          </h3>
          <p class="mt-3 text-base leading-relaxed text-slate-300">
            Jamming blinds satellite links. Spoofing corrupts navigation signals.
            Ground stations lose track of their assets at the worst possible moment.
            Traditional systems detect too late.
          </p>
        </div>

        <div class="rounded-2xl border border-blue-900/30 bg-blue-950/10 p-6 sm:p-8">
          <div class="mb-3 inline-flex items-center gap-2 text-sm font-semibold uppercase tracking-wider text-blue-400">
            <span class="inline-block size-2 rounded-full bg-blue-500"></span>
            Our answer
          </div>
          <h3 class="text-xl font-bold text-white sm:text-2xl">
            RF defense
          </h3>
          <p class="mt-3 text-base leading-relaxed text-slate-300">
            A space subsystem that continuously scans the spectrum,
            localizes threats, and applies protection — all onboard,
            in real time, without ground intervention.
          </p>
        </div>
      </div>

      <!-- === Les 3 modes === -->
      <div class="mt-16">
        <h2 class="text-center text-2xl font-bold text-white sm:text-3xl">
          Three modes. One defense loop.
        </h2>
        <p class="mx-auto mt-3 max-w-2xl text-center text-base text-slate-300 sm:text-lg">
          Bastion Space operates as a closed loop: from detection to satellite protection.
        </p>

        <div ref="statsRef" class="mt-10 grid gap-4 sm:grid-cols-3">
          <div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6 text-center">
            <div class="text-5xl font-bold text-white">{{ animated.modes }}</div>
            <div class="mt-3 text-base uppercase tracking-wider text-slate-300">Modes</div>
            <p class="mt-1 text-sm text-slate-400">Detect · Localize · Protect</p>
          </div>
          <div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6 text-center">
            <div class="text-5xl font-bold text-white">{{ animated.awareness }}°</div>
            <div class="mt-3 text-base uppercase tracking-wider text-slate-300">Awareness</div>
            <p class="mt-1 text-sm text-slate-400">Full RF spectrum surveillance</p>
          </div>
          <div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6 text-center">
            <div class="text-5xl font-bold text-white">{{ animated.latency }}s</div>
            <div class="mt-3 text-base uppercase tracking-wider text-slate-300">Latency</div>
            <p class="mt-1 text-sm text-slate-400">Real-time protection</p>
          </div>
        </div>
      </div>

      <!-- === Pourquoi nous === -->
      <div class="mt-16 grid gap-4 sm:grid-cols-3">
        <div class="rounded-lg border border-slate-800/60 bg-slate-900/20 p-6">
          <div class="text-base font-semibold text-white">Sovereign by design</div>
          <p class="mt-2 text-sm leading-relaxed text-slate-400">
            100% European technology. No foreign dependency on critical defense layers.
          </p>
        </div>
        <div class="rounded-lg border border-slate-800/60 bg-slate-900/20 p-6">
          <div class="text-base font-semibold text-white">Space-qualified</div>
          <p class="mt-2 text-sm leading-relaxed text-slate-400">
            Built to survive launch, radiation, and thermal cycling in orbit.
          </p>
        </div>
        <div class="rounded-lg border border-slate-800/60 bg-slate-900/20 p-6">
          <div class="text-base font-semibold text-white">Always on</div>
          <p class="mt-2 text-sm leading-relaxed text-slate-400">
            Continuous protection — not a reactive response after the link is lost.
          </p>
        </div>
      </div>

      <p class="mt-16 text-center text-base text-slate-400">
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
        animateValue('modes', 3, 2200)
        animateValue('awareness', 360, 2000)
        animateValue('latency', 2, 2000)
        observer.disconnect()
      }
    },
    { threshold: 0.3 }
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