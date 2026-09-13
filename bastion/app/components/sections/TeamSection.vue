<template>
  <section
    id="team"
    class="scroll-mt-20 px-4 py-20 sm:px-6 sm:py-24 lg:px-8"
  >
    <div class="mx-auto max-w-6xl">
      <!-- En-tête centré -->
      <div class="text-center">
        <h2 class="text-3xl font-bold tracking-tight text-white sm:text-4xl">
          Team
        </h2>
        <p class="mx-auto mt-4 max-w-2xl text-base text-slate-400 sm:text-lg">
          The team behind Bastion Space's R&D and strategy.
        </p>
      </div>

      <ul class="mt-12 flex flex-wrap justify-center gap-8 sm:gap-10">
        <li
          v-for="(member, i) in team"
          :key="i"
          class="flex w-full max-w-xs flex-col items-center text-center sm:max-w-sm"
        >
          <a
            :href="member.linkedin || '#'"
            :target="member.linkedin ? '_blank' : ''"
            :rel="member.linkedin ? 'noopener noreferrer' : ''"
            class="group relative aspect-square w-full max-w-[180px] overflow-hidden rounded-xl border border-slate-700 bg-slate-800 block sm:max-w-[200px]"
          >
            <img
              v-if="member.photo"
              :src="member.photo"
              :alt="member.name"
              class="size-full object-cover object-center transition group-hover:opacity-60"
            >
            <div
              v-else
              class="flex size-full items-center justify-center text-slate-600"
              aria-hidden
            >
              <svg class="size-12" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z" />
              </svg>
            </div>
            <div
              v-if="member.linkedin"
              class="absolute inset-0 flex items-center justify-center opacity-0 transition group-hover:opacity-100"
            >
              <svg class="size-10 text-white" fill="currentColor" viewBox="0 0 24 24">
                <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
              </svg>
            </div>
          </a>

          <p class="mt-4 text-xl font-semibold text-white sm:text-2xl">
            {{ member.name }}
          </p>

          <p class="mt-1 text-sm font-medium text-blue-400 sm:text-base">
            {{ member.role }}
          </p>

          <p class="mt-2 max-w-xs text-sm leading-relaxed text-slate-400 sm:text-base">
            {{ member.description }}
          </p>
        </li>
      </ul>

      <!-- Badge incubateur centré + cliquable -->
      <div class="mt-12 text-center">
        <a
          href="https://www.bordeaux-inp.fr/fr/lincubateur-bordeaux-inpulse"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-2 rounded-full border border-slate-700 bg-slate-800/50 px-4 py-1.5 text-xs font-medium text-slate-300 transition hover:border-blue-500/50 hover:bg-slate-800 hover:text-blue-300 sm:text-sm"
        >
          <svg class="size-3.5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25" />
          </svg>
          Incubated at Bordeaux INPulse
        </a>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const config = useRuntimeConfig()
const baseURL = config.app.baseURL

const teamData = [
  {
    name: 'Kichi-Tawa Bourguinat',
    role: 'Project Lead',
    description: 'Telecommunication Engineering Student at ENSEIRB-MATMECA, Bordeaux.',
    photo: 'images/ktb_portrait.jpg',
    linkedin: 'https://www.linkedin.com/in/kitchi-tawa-bourguinat',
  },
]

const team = computed(() =>
  teamData.map(m => ({
    ...m,
    photo: m.photo ? (baseURL + m.photo) : '',
  }))
)
</script>