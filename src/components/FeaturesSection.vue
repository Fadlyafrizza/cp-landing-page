<script setup>
import { RouterLink } from 'vue-router'

const features = [
  {
    icon: '⚡',
    title: 'Lightning Fast',
    desc: 'Optimized for performance with sub-second load times, ensuring the best user experience on all devices.',
  },
  {
    icon: '🛡️',
    title: 'Enterprise Security',
    desc: 'Bank-level security protocols, SSL certificates, and regular security audits to protect your data.',
  },
  {
    icon: '📊',
    title: 'Data-Driven',
    desc: 'We make decisions backed by data and analytics, measuring success with KPIs that matter.',
  },
  {
    icon: '🎯',
    title: 'Results-Focused',
    desc: 'Every project is aligned with your business goals. We deliver measurable outcomes, not just code.',
  },
  {
    icon: '🔄',
    title: 'Agile Process',
    desc: 'Flexible, iterative development with regular check-ins ensures projects stay on track and on budget.',
  },
  {
    icon: '🤝',
    title: 'Dedicated Support',
    desc: '24/7 support and maintenance with a dedicated account manager for enterprise clients.',
  },
  {
    icon: '🌐',
    title: 'Global Scale',
    desc: 'Infrastructure that scales globally, from startup MVP to enterprise-level with millions of users.',
  },
  {
    icon: '💡',
    title: 'Innovation First',
    desc: 'We stay ahead of technology trends so you can leverage the latest innovations for your business.',
  },
]
</script>

<template>
  <section id="features" class="py-24 lg:py-32 relative overflow-hidden" style="background: linear-gradient(180deg, #0f172a 0%, #0a0f1e 100%);">
    <!-- Background decoration -->
    <div class="absolute left-0 top-1/2 -translate-y-1/2 w-96 h-96 bg-cyan-400/5 rounded-full blur-3xl"></div>
    <div class="absolute right-0 bottom-0 w-64 h-64 bg-blue-600/5 rounded-full blur-3xl"></div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
      <div class="text-center mb-16" data-aos="fade-up">
        <span class="inline-block text-cyan-400 font-semibold text-sm tracking-widest uppercase mb-3">Why Choose Us</span>
        <h2 class="section-title text-3xl sm:text-4xl lg:text-5xl text-white mb-4">
          What Sets Us <span class="gradient-text">Apart</span>
        </h2>
        <p class="text-slate-400 text-lg max-w-2xl mx-auto">
          We don't just build products — we build partnerships. Here's why leading companies trust Nexora.
        </p>
      </div>

      <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <div
          v-for="(feature, i) in features"
          :key="i"
          class="feature-item glass-card p-6 group"
          data-aos="fade-up"
          :data-aos-delay="i * 60"
        >
          <div class="feature-icon-wrap mb-5">
            <span class="text-2xl">{{ feature.icon }}</span>
          </div>
          <h3 class="text-white font-bold text-lg mb-2 group-hover:text-cyan-400 transition-colors duration-300">
            {{ feature.title }}
          </h3>
          <p class="text-slate-400 text-sm leading-relaxed">
            {{ feature.desc }}
          </p>
        </div>
      </div>

      <!-- CTA Banner -->
      <div class="mt-20 glass-card p-10 lg:p-14 text-center" data-aos="fade-up">
        <h3 class="text-2xl sm:text-3xl lg:text-4xl font-black text-white mb-4">
          Ready to Transform Your <span class="gradient-text">Business?</span>
        </h3>
        <p class="text-slate-400 text-lg mb-8 max-w-xl mx-auto">
          Join 500+ companies that have trusted Nexora to power their digital growth.
        </p>
        <div class="flex flex-wrap justify-center gap-4">
          <RouterLink to="/contact" class="btn-primary inline-flex items-center gap-2">
            <span>Start a Project</span>
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
            </svg>
          </RouterLink>
          <RouterLink to="/contact" class="btn-outline inline-flex items-center gap-2">
            <span>Schedule a Call</span>
          </RouterLink>
        </div>
      </div>
    </div>
  </section>
</template>

