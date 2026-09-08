<template>
  <section
    id="home"
    class="relative flex min-h-screen flex-col justify-center overflow-hidden bg-gradient-to-b from-slate-900/80 to-transparent px-4 py-24 sm:px-6 sm:py-32 lg:px-8"
  >
    <div class="absolute inset-0 bg-[radial-gradient(ellipse_80%_50%_at_50%_-20%,rgba(59,130,246,0.15),transparent)]" />

    <div class="relative mx-auto max-w-4xl text-center">
      <!-- Badge "Next-gen space defense" -->
      <div class="mb-6 inline-block rounded-full border border-sky-500/20 bg-sky-500/10 px-4 py-1.5 text-xs font-medium text-sky-400 backdrop-blur-sm">
        Next-gen space defense
      </div>

      <h1 class="text-5xl font-bold tracking-tight sm:text-6xl lg:text-7xl">
        <span class="bg-gradient-to-r from-blue-400 via-sky-300 to-blue-400 bg-clip-text text-transparent">
          Bastion Space
        </span>
      </h1>

      <p class="mt-4 text-xl font-medium text-slate-300 sm:text-2xl">
        Detection, <span class="text-blue-400">anti-jamming</span> and <span class="text-blue-400">anti-spoofing</span>
      </p>
      <p class="mt-2 text-lg text-slate-400 sm:text-xl">
        for the protection of space communications
      </p>

      <!-- Description -->
      <p class="mx-auto mt-6 max-w-2xl text-base text-slate-500 sm:text-lg">
        We design cutting-edge solutions for sovereignty and security in space.
      </p>

      <!-- Boutons (agrandis avec icônes) -->
      <div class="mt-10 flex flex-wrap justify-center gap-4">
        <a
          href="#solution"
          class="inline-flex items-center gap-2 rounded-lg bg-blue-600 px-8 py-4 text-base font-medium text-white transition hover:bg-blue-500 hover:scale-105"
          @click.prevent="scrollTo('solution')"
        >
          <svg class="size-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M15.042 21.672L13.684 16.6m0 0l-2.51 2.225.569-9.47 5.227 7.917-3.286-.672zM12 2.25V4.5m5.834.166l-1.591 1.591M20.25 10.5H18M7.757 14.743l-1.59 1.59M6 10.5H3.75m4.007-4.243l-1.59-1.59" />
          </svg>
          Discover
        </a>
        <a
          href="#contact"
          class="inline-flex items-center gap-2 rounded-lg border border-slate-600 px-8 py-4 text-base font-medium text-slate-300 transition hover:border-slate-400 hover:bg-slate-800/50 hover:scale-105"
          @click.prevent="scrollTo('contact')"
        >
          <svg class="size-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75" />
          </svg>
          Contact us
        </a>
      </div>

      <!-- Statistiques / valeurs clés -->
      <div class="mt-16 grid grid-cols-1 gap-6 border-t border-slate-800/50 pt-8 sm:grid-cols-3">
        <div>
          <p class="text-3xl font-bold text-white">100%</p>
          <p class="text-sm text-slate-500">Sovereign technology</p>
        </div>
        <div>
          <p class="text-3xl font-bold text-white">24/7</p>
          <p class="text-sm text-slate-500">Protection</p>
        </div>
        <div>
          <p class="text-3xl font-bold text-white">Next-gen</p>
          <p class="text-sm text-slate-500">Anti-jamming solutions</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
function scrollTo (id: string) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>