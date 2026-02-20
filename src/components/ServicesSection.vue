<script setup>
const services = [
  {
    icon: '💻',
    title: 'Web Development',
    desc: 'Modern, fast, and scalable web applications built with the latest technologies like React, Vue, and Node.js.',
    tags: ['React', 'Vue', 'Node.js'],
    color: 'from-blue-600/20 to-cyan-400/10',
    border: 'hover:border-blue-400/50',
  },
  {
    icon: '📱',
    title: 'Mobile Apps',
    desc: 'Cross-platform mobile applications for iOS and Android with exceptional user experiences.',
    tags: ['React Native', 'Flutter', 'iOS/Android'],
    color: 'from-purple-600/20 to-pink-400/10',
    border: 'hover:border-purple-400/50',
  },
  {
    icon: '🎨',
    title: 'UI/UX Design',
    desc: 'Beautiful, intuitive interfaces that delight users and drive engagement with thoughtful design systems.',
    tags: ['Figma', 'Design Systems', 'Prototyping'],
    color: 'from-pink-600/20 to-rose-400/10',
    border: 'hover:border-pink-400/50',
  },
  {
    icon: '📈',
    title: 'Digital Marketing',
    desc: 'Data-driven marketing strategies that increase visibility, traffic, and conversions for your business.',
    tags: ['SEO', 'PPC', 'Social Media'],
    color: 'from-amber-600/20 to-orange-400/10',
    border: 'hover:border-amber-400/50',
  },
  {
    icon: '☁️',
    title: 'Cloud Solutions',
    desc: 'Scalable cloud infrastructure, DevOps automation, and managed services on AWS, GCP, and Azure.',
    tags: ['AWS', 'GCP', 'DevOps'],
    color: 'from-teal-600/20 to-cyan-400/10',
    border: 'hover:border-teal-400/50',
  },
  {
    icon: '🧩',
    title: 'IT Consulting',
    desc: 'Strategic technology consulting to help you make the right decisions and navigate digital transformation.',
    tags: ['Strategy', 'Architecture', 'Audit'],
    color: 'from-indigo-600/20 to-blue-400/10',
    border: 'hover:border-indigo-400/50',
  },
]
</script>

<template>
  <section id="services" class="py-24 lg:py-32 relative" style="background: linear-gradient(180deg, #0d1526 0%, #0f172a 100%);">
    <div class="absolute inset-0 opacity-5"
      style="background: radial-gradient(ellipse at center, #1e40af, transparent 70%);">
    </div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
      <div class="text-center mb-16" data-aos="fade-up">
        <span class="inline-block text-cyan-400 font-semibold text-sm tracking-widest uppercase mb-3">What We Do</span>
        <h2 class="section-title text-3xl sm:text-4xl lg:text-5xl text-white mb-4">
          Our <span class="gradient-text">Services</span>
        </h2>
        <p class="text-slate-400 text-lg max-w-2xl mx-auto">
          Comprehensive digital solutions tailored to your unique business needs. From concept to launch and beyond.
        </p>
      </div>

      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6 lg:gap-8">
        <div
          v-for="(service, i) in services"
          :key="i"
          class="service-card p-8 group"
          :class="service.border"
          data-aos="fade-up"
          :data-aos-delay="i * 80"
        >
          <div
            class="w-16 h-16 rounded-2xl mb-6 flex items-center justify-center text-3xl service-icon transition-all duration-300"
            :class="`bg-gradient-to-br ${service.color}`"
          >
            {{ service.icon }}
          </div>
          <h3 class="text-white font-bold text-xl mb-3 group-hover:text-cyan-400 transition-colors duration-300">
            {{ service.title }}
          </h3>
          <p class="text-slate-400 text-sm leading-relaxed mb-5">
            {{ service.desc }}
          </p>
          <div class="flex flex-wrap gap-2">
            <span
              v-for="tag in service.tags"
              :key="tag"
              class="text-xs px-3 py-1 rounded-full bg-white/5 text-slate-300 border border-white/10 group-hover:border-cyan-400/30 transition-colors duration-300"
            >
              {{ tag }}
            </span>
          </div>
          <div class="mt-6 flex items-center gap-2 text-cyan-400 text-sm font-medium opacity-0 group-hover:opacity-100 translate-y-2 group-hover:translate-y-0 transition-all duration-300">
            <span>Learn more</span>
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
            </svg>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
