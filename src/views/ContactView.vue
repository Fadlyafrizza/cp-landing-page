<script setup>
import { ref, reactive } from 'vue'
import { RouterLink } from 'vue-router'
import Navbar from '../components/Navbar.vue'
import FooterSection from '../components/FooterSection.vue'

const WEB3FORMS_KEY = import.meta.env.VITE_WEB3FORMS_KEY
const CONTACT_EMAIL = import.meta.env.VITE_CONTACT_EMAIL

const form = reactive({
  name: '',
  email: '',
  phone: '',
  subject: '',
  message: '',
})

const errors = reactive({
  name: '',
  email: '',
  phone: '',
  subject: '',
  message: '',
})

const status = ref('idle') // idle | loading | success | error
const errorMsg = ref('')

function validateEmail(email) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

function validatePhone(phone) {
  if (!phone) return true // phone is optional
  return /^[+\d\s\-()]{7,20}$/.test(phone)
}

function validate() {
  let valid = true
  Object.keys(errors).forEach((k) => (errors[k] = ''))

  if (!form.name.trim()) {
    errors.name = 'Name is required.'
    valid = false
  }
  if (!form.email.trim()) {
    errors.email = 'Email is required.'
    valid = false
  } else if (!validateEmail(form.email)) {
    errors.email = 'Please enter a valid email address.'
    valid = false
  }
  if (form.phone && !validatePhone(form.phone)) {
    errors.phone = 'Please enter a valid phone number.'
    valid = false
  }
  if (!form.subject.trim()) {
    errors.subject = 'Subject is required.'
    valid = false
  }
  if (!form.message.trim()) {
    errors.message = 'Message is required.'
    valid = false
  } else if (form.message.trim().length < 10) {
    errors.message = 'Message must be at least 10 characters.'
    valid = false
  }
  return valid
}

async function submitForm() {
  if (!validate()) return

  status.value = 'loading'
  errorMsg.value = ''

  try {
    const payload = {
      access_key: WEB3FORMS_KEY,
      to: CONTACT_EMAIL,
      name: form.name,
      email: form.email,
      phone: form.phone || 'N/A',
      subject: form.subject,
      message: form.message,
      from_name: 'Nexora Contact Form',
    }

    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
      body: JSON.stringify(payload),
    })

    const result = await response.json()

    if (result.success) {
      status.value = 'success'
      // Reset form
      Object.keys(form).forEach((k) => (form[k] = ''))
    } else {
      status.value = 'error'
      errorMsg.value = result.message || 'Something went wrong. Please try again.'
    }
  } catch {
    status.value = 'error'
    errorMsg.value = 'Network error. Please check your connection and try again.'
  }
}

function resetStatus() {
  status.value = 'idle'
  errorMsg.value = ''
}

const contactInfo = [
  {
    icon: '📧',
    title: 'Email Us',
    value: 'vadliafrizza80@gmail.com',
    href: 'mailto:vadliafrizza80@gmail.com',
    desc: 'Send us an email anytime',
  },
  {
    icon: '📞',
    title: 'Call Us',
    value: '+1 (555) 123-4567',
    href: 'tel:+15551234567',
    desc: 'Mon–Fri 9am to 6pm',
  },
  {
    icon: '📍',
    title: 'Visit Us',
    value: '123 Tech Street, San Francisco, CA 94105',
    href: '#',
    desc: 'Come say hello at our office',
  },
  {
    icon: '💬',
    title: 'WhatsApp',
    value: '+62 812-3456-7890',
    href: 'https://wa.me/6281234567890',
    desc: 'Chat with us on WhatsApp',
  },
]
</script>

<template>
  <div class="min-h-screen" style="background: #0f172a;">
    <Navbar />

    <!-- Page Header -->
    <section class="pt-28 pb-16 hero-bg relative overflow-hidden">
      <div class="absolute inset-0 opacity-5"
        style="background-image: linear-gradient(rgba(6,182,212,0.5) 1px, transparent 1px), linear-gradient(90deg, rgba(6,182,212,0.5) 1px, transparent 1px); background-size: 60px 60px;">
      </div>
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center relative">
        <span class="inline-block text-cyan-400 font-semibold text-sm tracking-widest uppercase mb-3">Get In Touch</span>
        <h1 class="text-4xl sm:text-5xl lg:text-6xl font-black text-white mb-4">
          Let's <span class="gradient-text">Connect</span>
        </h1>
        <p class="text-slate-400 text-lg max-w-xl mx-auto">
          Have a project in mind? We'd love to hear about it. Send us a message and we'll get back to you within 24 hours.
        </p>
        <div class="flex justify-center mt-6">
          <RouterLink to="/" class="text-cyan-400 text-sm hover:text-cyan-300 transition-colors flex items-center gap-1">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
            </svg>
            Back to Home
          </RouterLink>
        </div>
      </div>
    </section>

    <!-- Main content -->
    <section class="py-16 lg:py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid lg:grid-cols-5 gap-12">
          <!-- Contact Info Sidebar -->
          <div class="lg:col-span-2">
            <h2 class="text-2xl font-bold text-white mb-2">Contact Information</h2>
            <p class="text-slate-400 text-sm mb-8">Fill out the form or reach us directly through one of the channels below.</p>

            <div class="space-y-4 mb-10">
              <a
                v-for="info in contactInfo"
                :key="info.title"
                :href="info.href"
                class="glass-card p-5 flex items-start gap-4 group cursor-pointer block no-underline"
                :target="info.href.startsWith('http') ? '_blank' : undefined"
                :rel="info.href.startsWith('http') ? 'noopener noreferrer' : undefined"
              >
                <div class="text-2xl shrink-0 group-hover:scale-110 transition-transform duration-300">{{ info.icon }}</div>
                <div>
                  <div class="text-white font-semibold text-sm mb-0.5">{{ info.title }}</div>
                  <div class="text-cyan-400 text-sm font-medium">{{ info.value }}</div>
                  <div class="text-slate-500 text-xs mt-0.5">{{ info.desc }}</div>
                </div>
              </a>
            </div>

            <!-- Map placeholder -->
            <div class="glass-card overflow-hidden rounded-2xl">
              <div class="bg-gradient-to-br from-slate-800 to-slate-900 h-48 flex items-center justify-center relative">
                <div class="absolute inset-0 opacity-20"
                  style="background-image: linear-gradient(rgba(6,182,212,0.3) 1px, transparent 1px), linear-gradient(90deg, rgba(6,182,212,0.3) 1px, transparent 1px); background-size: 30px 30px;">
                </div>
                <div class="text-center z-10">
                  <div class="text-4xl mb-2">📍</div>
                  <div class="text-white font-semibold text-sm">San Francisco, CA</div>
                  <div class="text-slate-400 text-xs mt-1">123 Tech Street</div>
                </div>
              </div>
            </div>

            <!-- Business hours -->
            <div class="glass-card p-5 mt-4">
              <h3 class="text-white font-semibold text-sm mb-3 flex items-center gap-2">
                <span>🕒</span> Business Hours
              </h3>
              <div class="space-y-2">
                <div class="flex justify-between text-sm">
                  <span class="text-slate-400">Monday – Friday</span>
                  <span class="text-white">9:00 AM – 6:00 PM</span>
                </div>
                <div class="flex justify-between text-sm">
                  <span class="text-slate-400">Saturday</span>
                  <span class="text-white">10:00 AM – 4:00 PM</span>
                </div>
                <div class="flex justify-between text-sm">
                  <span class="text-slate-400">Sunday</span>
                  <span class="text-slate-500">Closed</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="lg:col-span-3">
            <div class="glass-card p-8 lg:p-10">
              <h2 class="text-2xl font-bold text-white mb-2">Send a Message</h2>
              <p class="text-slate-400 text-sm mb-8">All fields marked with * are required.</p>

              <!-- Success Message -->
              <Transition name="mobile-menu">
                <div v-if="status === 'success'" class="mb-6 p-5 rounded-xl bg-green-500/10 border border-green-500/30 flex items-start gap-4">
                  <div class="text-2xl shrink-0">✅</div>
                  <div>
                    <div class="text-green-400 font-bold mb-1">Message Sent Successfully!</div>
                    <div class="text-slate-400 text-sm">Thank you for reaching out. We'll get back to you within 24 hours.</div>
                    <button @click="resetStatus" class="text-cyan-400 text-sm mt-2 hover:underline">Send another message</button>
                  </div>
                </div>
              </Transition>

              <!-- Error Message -->
              <Transition name="mobile-menu">
                <div v-if="status === 'error'" class="mb-6 p-5 rounded-xl bg-red-500/10 border border-red-500/30 flex items-start gap-4">
                  <div class="text-2xl shrink-0">❌</div>
                  <div>
                    <div class="text-red-400 font-bold mb-1">Failed to Send Message</div>
                    <div class="text-slate-400 text-sm">{{ errorMsg }}</div>
                    <button @click="resetStatus" class="text-cyan-400 text-sm mt-2 hover:underline">Try again</button>
                  </div>
                </div>
              </Transition>

              <form v-if="status !== 'success'" @submit.prevent="submitForm" novalidate>
                <div class="grid sm:grid-cols-2 gap-5 mb-5">
                  <!-- Name -->
                  <div>
                    <label class="block text-slate-300 text-sm font-medium mb-2">Full Name *</label>
                    <input
                      v-model="form.name"
                      type="text"
                      placeholder="John Smith"
                      class="form-input"
                      :class="{ error: errors.name }"
                      @input="errors.name = ''"
                    />
                    <p v-if="errors.name" class="text-red-400 text-xs mt-1">{{ errors.name }}</p>
                  </div>

                  <!-- Email -->
                  <div>
                    <label class="block text-slate-300 text-sm font-medium mb-2">Email Address *</label>
                    <input
                      v-model="form.email"
                      type="email"
                      placeholder="john@example.com"
                      class="form-input"
                      :class="{ error: errors.email }"
                      @input="errors.email = ''"
                    />
                    <p v-if="errors.email" class="text-red-400 text-xs mt-1">{{ errors.email }}</p>
                  </div>

                  <!-- Phone -->
                  <div>
                    <label class="block text-slate-300 text-sm font-medium mb-2">Phone Number</label>
                    <input
                      v-model="form.phone"
                      type="tel"
                      placeholder="+1 (555) 123-4567"
                      class="form-input"
                      :class="{ error: errors.phone }"
                      @input="errors.phone = ''"
                    />
                    <p v-if="errors.phone" class="text-red-400 text-xs mt-1">{{ errors.phone }}</p>
                  </div>

                  <!-- Subject -->
                  <div>
                    <label class="block text-slate-300 text-sm font-medium mb-2">Subject *</label>
                    <select
                      v-model="form.subject"
                      class="form-input"
                      :class="{ error: errors.subject }"
                      @change="errors.subject = ''"
                    >
                      <option value="" disabled>Select a subject</option>
                      <option>Web Development Project</option>
                      <option>Mobile App Development</option>
                      <option>UI/UX Design</option>
                      <option>Digital Marketing</option>
                      <option>Cloud Solutions</option>
                      <option>IT Consulting</option>
                      <option>General Inquiry</option>
                      <option>Other</option>
                    </select>
                    <p v-if="errors.subject" class="text-red-400 text-xs mt-1">{{ errors.subject }}</p>
                  </div>
                </div>

                <!-- Message -->
                <div class="mb-6">
                  <label class="block text-slate-300 text-sm font-medium mb-2">Message *</label>
                  <textarea
                    v-model="form.message"
                    rows="6"
                    placeholder="Tell us about your project, goals, and timeline..."
                    class="form-input resize-none"
                    :class="{ error: errors.message }"
                    @input="errors.message = ''"
                  ></textarea>
                  <p v-if="errors.message" class="text-red-400 text-xs mt-1">{{ errors.message }}</p>
                  <p class="text-slate-500 text-xs mt-1">{{ form.message.length }} / 2000 characters</p>
                </div>

                <!-- Submit -->
                <button
                  type="submit"
                  :disabled="status === 'loading'"
                  class="btn-primary w-full flex items-center justify-center gap-3 text-base disabled:opacity-60 disabled:cursor-not-allowed"
                >
                  <span v-if="status === 'loading'" class="w-5 h-5 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
                  <span>{{ status === 'loading' ? 'Sending...' : 'Send Message' }}</span>
                  <svg v-if="status !== 'loading'" class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
                  </svg>
                </button>

                <p class="text-slate-500 text-xs text-center mt-4">
                  By submitting this form you agree to our
                  <a href="#" class="text-cyan-400 hover:underline">Privacy Policy</a>.
                  We'll never share your information.
                </p>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <FooterSection />
  </div>
</template>
