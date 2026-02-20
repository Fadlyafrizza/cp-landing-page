<script setup>
import { ref } from 'vue'

const current = ref(0)

const testimonials = [
  {
    name: 'Sarah Johnson',
    role: 'CEO, TechStartup Inc.',
    avatar: 'SJ',
    rating: 5,
    text: 'Nexora completely transformed our digital presence. The team delivered our new platform 2 weeks ahead of schedule and the results exceeded every expectation. Our user engagement increased by 340% in just 3 months.',
    company: 'TechStartup',
  },
  {
    name: 'Michael Chen',
    role: 'CTO, E-Commerce Giant',
    avatar: 'MC',
    rating: 5,
    text: 'We\'ve worked with many agencies over the years, but Nexora is on another level. Their technical expertise, attention to detail, and proactive communication make them the ideal long-term partner.',
    company: 'ShopNow',
  },
  {
    name: 'Emily Rodriguez',
    role: 'Marketing Director, FinTech Co.',
    avatar: 'ER',
    rating: 5,
    text: 'The mobile app Nexora built for us has over 200,000 active users and a 4.9-star app store rating. Their UI/UX design team truly understands how to create products people love.',
    company: 'PayFlow',
  },
  {
    name: 'David Park',
    role: 'Founder, SaaS Platform',
    avatar: 'DP',
    rating: 5,
    text: 'From concept to launch in just 6 weeks — Nexora made our vision a reality. Their cloud infrastructure is bulletproof and scales effortlessly as we grow.',
    company: 'CloudDesk',
  },
  {
    name: 'Lisa Thompson',
    role: 'VP Product, Healthcare Tech',
    avatar: 'LT',
    rating: 5,
    text: 'Nexora\'s consulting team helped us navigate a complex digital transformation. Their strategic guidance saved us from costly mistakes and put us 18 months ahead of competitors.',
    company: 'MedTech',
  },
]

function prev() {
  current.value = (current.value - 1 + testimonials.length) % testimonials.length
}

function next() {
  current.value = (current.value + 1) % testimonials.length
}

function goTo(i) {
  current.value = i
}

const colors = ['from-blue-600 to-cyan-400', 'from-purple-600 to-pink-400', 'from-teal-600 to-green-400', 'from-orange-600 to-amber-400', 'from-rose-600 to-pink-400']
</script>

<template>
  <section id="testimonials" class="py-24 lg:py-32 relative overflow-hidden" style="background: linear-gradient(180deg, #0a0f1e 0%, #0f172a 100%);">
    <div class="absolute inset-0 opacity-5"
      style="background: radial-gradient(ellipse at 50% 50%, #06b6d4, transparent 70%);">
    </div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
      <div class="text-center mb-16" data-aos="fade-up">
        <span class="inline-block text-cyan-400 font-semibold text-sm tracking-widest uppercase mb-3">Testimonials</span>
        <h2 class="section-title text-3xl sm:text-4xl lg:text-5xl text-white mb-4">
          What Our <span class="gradient-text">Clients Say</span>
        </h2>
        <p class="text-slate-400 text-lg max-w-2xl mx-auto">
          Don't just take our word for it — hear from the companies that have partnered with us.
        </p>
      </div>

      <!-- Main testimonial -->
      <div class="relative max-w-4xl mx-auto" data-aos="fade-up">
        <div class="glass-card p-8 lg:p-12 text-center transition-all duration-500">
          <!-- Quote icon -->
          <div class="text-6xl text-cyan-400/20 font-serif leading-none mb-6 select-none">"</div>

          <!-- Stars -->
          <div class="flex justify-center mb-6">
            <svg v-for="i in testimonials[current].rating" :key="i" class="w-5 h-5 text-amber-400" fill="currentColor" viewBox="0 0 20 20">
              <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
            </svg>
          </div>

          <!-- Text -->
          <p class="text-slate-300 text-lg lg:text-xl leading-relaxed mb-8 max-w-2xl mx-auto italic">
            "{{ testimonials[current].text }}"
          </p>

          <!-- Author -->
          <div class="flex items-center justify-center gap-4">
            <div
              class="w-14 h-14 rounded-full flex items-center justify-center text-white font-bold text-lg bg-gradient-to-br"
              :class="colors[current % colors.length]"
            >
              {{ testimonials[current].avatar }}
            </div>
            <div class="text-left">
              <div class="text-white font-bold">{{ testimonials[current].name }}</div>
              <div class="text-cyan-400 text-sm">{{ testimonials[current].role }}</div>
            </div>
          </div>
        </div>

        <!-- Navigation arrows -->
        <button
          @click="prev"
          class="absolute -left-4 lg:-left-8 top-1/2 -translate-y-1/2 w-12 h-12 glass-card rounded-full flex items-center justify-center text-white hover:text-cyan-400 hover:border-cyan-400/40 transition-all duration-300 shadow-lg"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
          </svg>
        </button>
        <button
          @click="next"
          class="absolute -right-4 lg:-right-8 top-1/2 -translate-y-1/2 w-12 h-12 glass-card rounded-full flex items-center justify-center text-white hover:text-cyan-400 hover:border-cyan-400/40 transition-all duration-300 shadow-lg"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>
      </div>

      <!-- Dots -->
      <div class="flex justify-center gap-2 mt-8">
        <button
          v-for="(_, i) in testimonials"
          :key="i"
          @click="goTo(i)"
          class="rounded-full transition-all duration-300"
          :class="i === current ? 'w-8 h-2.5 bg-cyan-400' : 'w-2.5 h-2.5 bg-slate-600 hover:bg-slate-400'"
        ></button>
      </div>

      <!-- Mini testimonial cards -->
      <div class="grid sm:grid-cols-3 gap-4 mt-12">
        <div
          v-for="(t, i) in testimonials.slice(0, 3)"
          :key="i"
          class="glass-card p-5 cursor-pointer transition-all duration-300"
          :class="i === current % 3 ? 'border-cyan-400/30' : ''"
          @click="goTo(i)"
          data-aos="fade-up"
          :data-aos-delay="i * 100"
        >
          <div class="flex items-center gap-3 mb-3">
            <div
              class="w-10 h-10 rounded-full flex items-center justify-center text-white font-bold text-sm bg-gradient-to-br"
              :class="colors[i % colors.length]"
            >
              {{ t.avatar }}
            </div>
            <div>
              <div class="text-white font-semibold text-sm">{{ t.name }}</div>
              <div class="text-slate-400 text-xs">{{ t.company }}</div>
            </div>
          </div>
          <p class="text-slate-400 text-xs leading-relaxed line-clamp-2">{{ t.text }}</p>
        </div>
      </div>
    </div>
  </section>
</template>
