<template>
  <section
    id="team"
    class="scroll-mt-20 px-4 py-20 sm:px-6 sm:py-24 lg:px-8"
  >
    <div class="mx-auto max-w-6xl">
      <h2 class="text-3xl font-bold tracking-tight text-white sm:text-4xl">
        Team
      </h2>
      <p class="mt-4 max-w-2xl text-slate-400">
        The team behind Bastion Space's R&D and strategy.
      </p>
      <ul class="mt-12 flex flex-wrap justify-center gap-10">
        <li
          v-for="(member, i) in team"
          :key="i"
          class="flex flex-col items-center text-center"
        >
          <p class="mt-3 text-3xl font-semibold text-white truncate">
            {{ member.name }}
          </p>
          <p class="mt-0.5 text-lg text-slate-500">
            Telecommunication Engineering Student at ENSEIRB-MATMECA Bordeaux France · {{ member.role }}
          </p>
          <p class="mt-3 text-base text-slate-400 ">
            From ML jamming detection to business strategy.
          </p>
          <a
            :href="member.linkedin || '#'"
            :target="member.linkedin ? '_blank' : ''"
            :rel="member.linkedin ? 'noopener noreferrer' : ''"
            class="group relative mt-3 aspect-square w-full max-w-[280px] overflow-hidden rounded-xl border border-slate-700 bg-slate-800 block"
          >
            <img
              v-if="member.photo"
              :src="member.photo"
              :alt="member.name"
              class="size-full object-cover transition group-hover:opacity-60"
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
        </li>
      </ul>
    </div>
  </section>
</template>

<script setup lang="ts">
const config = useRuntimeConfig()
const baseURL = config.app.baseURL

const teamData = [
  { name: 'Kichi-Tawa BOURGUINAT', role: 'Project Lead', photo: 'images/team/ktb_portrait.jpg', linkedin: 'https://www.linkedin.com/in/kitchi-tawa-bourguinat' },
]

const team = computed(() =>
  teamData.map(m => ({
    ...m,
    photo: m.photo ? (baseURL + m.photo) : ''
  }))
)
</script>
