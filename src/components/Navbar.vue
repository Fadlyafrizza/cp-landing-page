<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { RouterLink, useRouter } from 'vue-router'

const router = useRouter()
const isScrolled = ref(false)
const mobileOpen = ref(false)

const navLinks = [
  { label: 'Home', href: '/#home' },
  { label: 'About', href: '/#about' },
  { label: 'Services', href: '/#services' },
  { label: 'Contact', href: '/contact' },
]

function handleScroll() {
  isScrolled.value = window.scrollY > 50
}

function toggleMobile() {
  mobileOpen.value = !mobileOpen.value
}

function closeMobile() {
  mobileOpen.value = false
}

function navigate(href) {
  closeMobile()
  if (href.startsWith('/#')) {
    const id = href.slice(2)
    if (router.currentRoute.value.path !== '/') {
      router.push('/').then(() => {
        setTimeout(() => {
          const el = document.getElementById(id)
          if (el) el.scrollIntoView({ behavior: 'smooth' })
        }, 300)
      })
    } else {
      const el = document.getElementById(id)
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    }
  } else {
    router.push(href)
  }
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="isScrolled ? 'navbar-blur shadow-lg shadow-black/20' : 'bg-transparent'"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16 lg:h-20">
        <!-- Logo -->
        <button @click="navigate('/#home')" class="flex items-center gap-2 group">
          <div class="w-9 h-9 rounded-xl bg-gradient-to-br from-cyan-400 to-blue-600 flex items-center justify-center shadow-lg shadow-cyan-500/30">
            <span class="text-white font-black text-lg leading-none">N</span>
          </div>
          <span class="text-xl font-black text-white group-hover:text-cyan-400 transition-colors duration-300">
            Nexora
          </span>
        </button>

        <!-- Desktop Nav -->
        <div class="hidden md:flex items-center gap-8">
          <button
            v-for="link in navLinks"
            :key="link.label"
            @click="navigate(link.href)"
            class="text-slate-300 hover:text-cyan-400 font-medium transition-colors duration-300 relative group text-sm"
          >
            {{ link.label }}
            <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-cyan-400 group-hover:w-full transition-all duration-300 rounded-full"></span>
          </button>
          <button
            @click="navigate('/contact')"
            class="btn-primary text-sm py-2.5 px-6"
          >
            Get Started
          </button>
        </div>

        <!-- Mobile hamburger -->
        <button
          @click="toggleMobile"
          class="md:hidden flex flex-col gap-1.5 w-8 h-8 justify-center items-center"
          aria-label="Toggle menu"
        >
          <span
            class="block w-6 h-0.5 bg-white transition-all duration-300"
            :class="mobileOpen ? 'rotate-45 translate-y-2' : ''"
          ></span>
          <span
            class="block w-6 h-0.5 bg-white transition-all duration-300"
            :class="mobileOpen ? 'opacity-0' : ''"
          ></span>
          <span
            class="block w-6 h-0.5 bg-white transition-all duration-300"
            :class="mobileOpen ? '-rotate-45 -translate-y-2' : ''"
          ></span>
        </button>
      </div>
    </div>

    <!-- Mobile Menu -->
    <Transition name="mobile-menu">
      <div
        v-if="mobileOpen"
        class="md:hidden navbar-blur border-t border-white/10"
      >
        <div class="px-4 py-4 flex flex-col gap-2">
          <button
            v-for="link in navLinks"
            :key="link.label"
            @click="navigate(link.href)"
            class="text-slate-300 hover:text-cyan-400 font-medium py-3 px-4 rounded-xl hover:bg-white/5 transition-all duration-200 text-left"
          >
            {{ link.label }}
          </button>
          <button
            @click="navigate('/contact')"
            class="btn-primary mt-2 text-center"
          >
            Get Started
          </button>
        </div>
      </div>
    </Transition>
  </nav>
</template>
