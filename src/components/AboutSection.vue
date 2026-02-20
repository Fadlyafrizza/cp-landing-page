<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const stats = [
  { value: 500, suffix: '+', label: 'Happy Clients', icon: '😊' },
  { value: 300, suffix: '+', label: 'Projects Done', icon: '🚀' },
  { value: 50, suffix: '+', label: 'Team Members', icon: '👥' },
  { value: 7, suffix: '+', label: 'Years Experience', icon: '🏆' },
]

const counters = ref(stats.map(() => 0))
const sectionRef = ref(null)
let started = false
let observer

function animateCounter(index, target) {
  const duration = 2000
  const step = target / (duration / 16)
  let current = 0
  const timer = setInterval(() => {
    current += step
    if (current >= target) {
      counters.value[index] = target
      clearInterval(timer)
    } else {
      counters.value[index] = Math.floor(current)
    }
  }, 16)
}

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting && !started) {
        started = true
        stats.forEach((s, i) => animateCounter(i, s.value))
      }
    },
    { threshold: 0.3 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<template>
  <section id="about" class="py-24 lg:py-32 relative overflow-hidden" style="background: linear-gradient(180deg, #0f172a 0%, #0d1526 100%);">
    <!-- BG decoration -->
    <div class="absolute top-0 right-0 w-1/3 h-full opacity-5"
      style="background: radial-gradient(ellipse at right, #06b6d4, transparent);">
    </div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Header -->
      <div class="text-center mb-16" data-aos="fade-up">
        <span class="inline-block text-cyan-400 font-semibold text-sm tracking-widest uppercase mb-3">About Us</span>
        <h2 class="section-title text-3xl sm:text-4xl lg:text-5xl text-white mb-4">
          Who We <span class="gradient-text">Are</span>
        </h2>
        <p class="text-slate-400 text-lg max-w-2xl mx-auto">
          We are a passionate team of digital innovators dedicated to transforming businesses through cutting-edge technology and creative design.
        </p>
      </div>

      <div class="grid lg:grid-cols-2 gap-16 items-center mb-20">
        <!-- Left - text -->
        <div data-aos="fade-right">
          <h3 class="text-2xl sm:text-3xl font-bold text-white mb-6 leading-tight">
            Building the Future of
            <span class="gradient-text"> Digital Experiences</span>
          </h3>
          <p class="text-slate-400 leading-relaxed mb-6">
            Founded in 2018, Nexora has grown from a small startup into a full-service digital agency serving clients worldwide. We combine technical expertise with creative thinking to deliver solutions that drive real business results.
          </p>
          <p class="text-slate-400 leading-relaxed mb-8">
            Our team of 50+ specialists works across web development, mobile applications, UI/UX design, digital marketing, and cloud solutions — all under one roof.
          </p>
          <div class="flex flex-wrap gap-4">
            <div class="flex items-center gap-2 text-slate-300">
              <svg class="w-5 h-5 text-cyan-400" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-sm">Agile methodology</span>
            </div>
            <div class="flex items-center gap-2 text-slate-300">
              <svg class="w-5 h-5 text-cyan-400" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-sm">On-time delivery</span>
            </div>
            <div class="flex items-center gap-2 text-slate-300">
              <svg class="w-5 h-5 text-cyan-400" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-sm">24/7 support</span>
            </div>
            <div class="flex items-center gap-2 text-slate-300">
              <svg class="w-5 h-5 text-cyan-400" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-sm">Industry expertise</span>
            </div>
          </div>
        </div>

        <!-- Right - visual -->
        <div data-aos="fade-left" class="relative">
          <div class="glass-card p-8 relative">
            <div class="absolute -top-4 -right-4 w-24 h-24 bg-gradient-to-br from-cyan-400/20 to-blue-600/20 rounded-2xl blur-xl"></div>
            <div class="grid grid-cols-2 gap-4">
              <div v-for="(item, i) in [
                { icon: '🌍', title: 'Global Reach', desc: 'Serving clients in 30+ countries' },
                { icon: '⚡', title: 'Fast Delivery', desc: 'Projects shipped 40% faster' },
                { icon: '🔒', title: 'Secure & Reliable', desc: '99.9% uptime guarantee' },
                { icon: '🎯', title: 'Goal Oriented', desc: 'Results-driven approach' },
              ]" :key="i"
                class="bg-white/5 rounded-xl p-4 hover:bg-white/8 transition-all duration-300 hover:scale-105"
              >
                <div class="text-2xl mb-2">{{ item.icon }}</div>
                <div class="text-white font-semibold text-sm mb-1">{{ item.title }}</div>
                <div class="text-slate-400 text-xs">{{ item.desc }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Stats counters -->
      <div ref="sectionRef" class="grid grid-cols-2 lg:grid-cols-4 gap-6">
        <div
          v-for="(stat, i) in stats"
          :key="i"
          class="stat-card p-6 lg:p-8 text-center"
          data-aos="zoom-in"
          :data-aos-delay="i * 100"
        >
          <div class="text-3xl mb-3">{{ stat.icon }}</div>
          <div class="text-3xl sm:text-4xl lg:text-5xl font-black gradient-text">
            {{ counters[i] }}{{ stat.suffix }}
          </div>
          <div class="text-slate-400 text-sm mt-2 font-medium">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>
