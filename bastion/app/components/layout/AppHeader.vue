<template>
  <header class="sticky top-0 z-50 border-b border-slate-800/80 bg-slate-950/90 backdrop-blur-sm">
    <nav class="mx-auto flex max-w-6xl items-center justify-between px-4 py-3 sm:px-6 lg:px-8">
      <NuxtLink
        to="/"
        class="flex items-center gap-2.5 transition hover:opacity-80"
        @click.prevent="scrollTo('home')"
      >
        <img :src="baseURL + 'images/logo.png'" alt="Bastion logo" class="size-8 object-contain" />
        <div class="flex flex-col leading-tight">
          <span class="text-lg font-bold tracking-tight text-white">Bastion<span class="text-blue-500">.</span></span>
          <span class="hidden text-[10px] font-medium uppercase tracking-widest text-slate-500 sm:block">Space RF Defense</span>
        </div>
      </NuxtLink>

      <ul class="hidden items-center gap-1 md:flex">
        <li v-for="item in navLinks" :key="item.id">
          
            :href="`#${item.id}`"
            class="relative rounded-md px-3 py-2 text-sm transition"
            :class="activeSection === item.id
              ? 'text-white'
              : 'text-slate-400 hover:text-slate-200'"
            @click.prevent="scrollTo(item.id)"
          >
            {{ item.label }}
            <span
              v-if="activeSection === item.id"
              class="absolute inset-x-1 -bottom-[13px] h-[2px] rounded-full bg-blue-500"
            />
          </a>
        </li>
        <li class="ml-4">
          
            href="#contact"
            class="rounded-lg bg-blue-600 px-4 py-2 text-sm font-medium text-white transition hover:bg-blue-500"
            @click.prevent="scrollTo('contact')"
          >
            Contact us
          </a>
        </li>
      </ul>

      <button
        type="button"
        class="rounded p-2 text-slate-400 hover:bg-slate-800 hover:text-white md:hidden"
        aria-label="Menu"
        @click="open = !open"
      >
        <svg class="size-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path v-if="!open" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </nav>

    <div
      v-show="open"
      class="border-t border-slate-800/80 bg-slate-900/95 px-4 py-4 md:hidden"
    >
      <ul class="flex flex-col gap-4">
        <li v-for="item in navLinks" :key="item.id">
          
            :href="`#${item.id}`"
            class="block transition"
            :class="activeSection === item.id
              ? 'text-white font-medium'
              : 'text-slate-400 hover:text-white'"
            @click.prevent="scrollTo(item.id); open = false"
          >
            {{ item.label }}
          </a>
        </li>
        <li>
          
            href="#contact"
            class="inline-block rounded-lg bg-blue-600 px-4 py-2 text-sm font-medium text-white transition hover:bg-blue-500"
            @click.prevent="scrollTo('contact'); open = false"
          >
            Contact us
          </a>
        </li>
      </ul>
    </div>
  </header>
</template>

<script setup lang="ts">
const config = useRuntimeConfig()
const baseURL = config.app.baseURL

const open = ref(false)
const activeSection = ref('home')

const sectionIds = ['home', 'solution', 'business', 'team', 'contact']

const navLinks = [
  { id: 'home', label: 'Home' },
  { id: 'solution', label: 'Solution' },
  { id: 'business', label: 'Business' },
  { id: 'team', label: 'Team' },
]

let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id
        }
      }
    },
    { rootMargin: '-40% 0px -55% 0px' }
  )

  for (const id of sectionIds) {
    const el = document.getElementById(id)
    if (el) observer.observe(el)
  }
})

onUnmounted(() => {
  observer?.disconnect()
})

function scrollTo (id: string) {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>
