<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const visible = ref(false)
const currentWord = ref(0)
const words = ['Innovation', 'Excellence', 'Growth', 'Success']
const displayWord = ref(words[0])

let wordInterval

function navigateContact() {
  router.push('/contact')
}

function scrollAbout() {
  const el = document.getElementById('about')
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}

function cycleWords() {
  wordInterval = setInterval(() => {
    currentWord.value = (currentWord.value + 1) % words.length
    displayWord.value = words[currentWord.value]
  }, 2500)
}

onMounted(() => {
  setTimeout(() => { visible.value = true }, 100)
  cycleWords()
})
</script>

<template>
  <section id="home" class="hero-bg min-h-screen flex items-center relative overflow-hidden">
    <!-- Decorative grid -->
    <div class="absolute inset-0 opacity-5">
      <div class="w-full h-full" style="background-image: linear-gradient(rgba(6,182,212,0.5) 1px, transparent 1px), linear-gradient(90deg, rgba(6,182,212,0.5) 1px, transparent 1px); background-size: 60px 60px;"></div>
    </div>

    <!-- Floating orbs -->
    <div class="absolute top-1/4 right-1/4 w-64 h-64 bg-blue-600/10 rounded-full blur-3xl animate-pulse"></div>
    <div class="absolute bottom-1/4 left-1/3 w-48 h-48 bg-cyan-400/10 rounded-full blur-3xl" style="animation: float 6s ease-in-out infinite;"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-24 pb-16 w-full z-10">
      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <!-- Left content -->
        <div
          class="transition-all duration-1000"
          :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
        >
          <div class="inline-flex items-center gap-2 bg-cyan-400/10 border border-cyan-400/20 rounded-full px-4 py-2 mb-6">
            <span class="w-2 h-2 bg-cyan-400 rounded-full animate-pulse"></span>
            <span class="text-cyan-400 text-sm font-medium">Professional Digital Solutions</span>
          </div>

          <h1 class="text-4xl sm:text-5xl lg:text-6xl xl:text-7xl font-black leading-tight mb-4 text-white">
            We Drive
            <br />
            <span class="gradient-text">Digital</span>
            <br />
            <span class="relative inline-block">
              <span class="gradient-text">{{ displayWord }}</span>
              <span class="inline-block w-1 h-12 lg:h-16 bg-cyan-400 ml-1 animate-pulse align-middle"></span>
            </span>
          </h1>

          <p
            class="text-slate-400 text-lg sm:text-xl max-w-lg mb-10 leading-relaxed transition-all duration-1000 delay-300"
            :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
          >
            Transform your business with cutting-edge digital solutions. We build
            exceptional web experiences, mobile apps, and scalable cloud solutions.
          </p>

          <div
            class="flex flex-wrap gap-4 transition-all duration-1000 delay-500"
            :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
          >
            <button @click="navigateContact" class="btn-primary flex items-center gap-2">
              <span>Start Your Project</span>
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
              </svg>
            </button>
            <button @click="scrollAbout" class="btn-outline flex items-center gap-2">
              <span>Learn More</span>
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
              </svg>
            </button>
          </div>

          <!-- Trust badges -->
          <div
            class="flex flex-wrap items-center gap-6 mt-12 transition-all duration-1000 delay-700"
            :class="visible ? 'opacity-100' : 'opacity-0'"
          >
            <div class="flex items-center gap-2">
              <div class="flex -space-x-2">
                <div v-for="i in 4" :key="i" class="w-8 h-8 rounded-full bg-gradient-to-br from-cyan-400 to-blue-600 border-2 border-slate-900 flex items-center justify-center text-xs font-bold text-white">
                  {{ String.fromCharCode(64 + i) }}
                </div>
              </div>
              <span class="text-slate-400 text-sm">500+ Happy Clients</span>
            </div>
            <div class="flex items-center gap-1.5">
              <div class="flex">
                <svg v-for="i in 5" :key="i" class="w-4 h-4 text-amber-400" fill="currentColor" viewBox="0 0 20 20">
                  <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                </svg>
              </div>
              <span class="text-slate-400 text-sm">5.0 Rating</span>
            </div>
          </div>
        </div>

        <!-- Right visual -->
        <div
          class="hidden lg:flex justify-center items-center relative transition-all duration-1000 delay-200"
          :class="visible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-10'"
        >
          <div class="relative w-96 h-96">
            <!-- Rotating ring -->
            <div class="absolute inset-0 rounded-full border-2 border-dashed border-cyan-400/20" style="animation: spin 20s linear infinite;"></div>
            <div class="absolute inset-8 rounded-full border-2 border-dashed border-blue-400/20" style="animation: spin 15s linear infinite reverse;"></div>

            <!-- Center card -->
            <div class="absolute inset-16 glass-card flex flex-col items-center justify-center p-6 text-center">
              <div class="text-5xl mb-3">🚀</div>
              <div class="text-white font-bold text-lg">Digital Agency</div>
              <div class="text-cyan-400 text-sm mt-1">Est. 2018</div>
            </div>

            <!-- Orbiting icons -->
            <div class="absolute -top-4 left-1/2 -translate-x-1/2 glass-card p-3 rounded-xl" style="animation: float 4s ease-in-out infinite;">
              <span class="text-2xl">💻</span>
            </div>
            <div class="absolute top-1/2 -right-4 -translate-y-1/2 glass-card p-3 rounded-xl" style="animation: float 5s ease-in-out infinite 1s;">
              <span class="text-2xl">📱</span>
            </div>
            <div class="absolute -bottom-4 left-1/2 -translate-x-1/2 glass-card p-3 rounded-xl" style="animation: float 6s ease-in-out infinite 0.5s;">
              <span class="text-2xl">☁️</span>
            </div>
            <div class="absolute top-1/2 -left-4 -translate-y-1/2 glass-card p-3 rounded-xl" style="animation: float 4.5s ease-in-out infinite 1.5s;">
              <span class="text-2xl">🎨</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 opacity-60">
      <span class="text-slate-400 text-xs">Scroll Down</span>
      <div class="w-6 h-10 rounded-full border-2 border-slate-600 flex justify-center pt-2">
        <div class="w-1.5 h-2.5 bg-cyan-400 rounded-full" style="animation: bounce 1.5s ease-in-out infinite;"></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
@keyframes bounce {
  0%, 100% { transform: translateY(0); opacity: 1; }
  50% { transform: translateY(8px); opacity: 0.5; }
}
</style>
