<script setup>
import { onMounted, onUnmounted } from 'vue'
import AOS from 'aos'
import 'aos/dist/aos.css'

import Navbar from '../components/Navbar.vue'
import HeroSection from '../components/HeroSection.vue'
import AboutSection from '../components/AboutSection.vue'
import ServicesSection from '../components/ServicesSection.vue'
import FeaturesSection from '../components/FeaturesSection.vue'
import TestimonialsSection from '../components/TestimonialsSection.vue'
import FooterSection from '../components/FooterSection.vue'
import WhatsAppButton from '../components/WhatsAppButton.vue'

onMounted(() => {
  AOS.init({
    duration: 700,
    easing: 'ease-out-cubic',
    once: true,
    offset: 60,
  })
})
</script>

<template>
  <div class="min-h-screen">
    <Navbar />
    <HeroSection />
    <AboutSection />
    <ServicesSection />
    <FeaturesSection />
    <TestimonialsSection />
    <FooterSection />
    <WhatsAppButton />
  </div>
</template>
