<template>
  <div>
    <!-- Navigation -->
    <nav class="bg-blue-500 p-4">
      <div class="container mx-auto flex justify-between items-center">
        <NuxtLink to="/" class="text-white text-xl font-bold">Logo</NuxtLink>
        <div class="hidden md:flex space-x-4">
          <NuxtLink to="/" class="text-white hover:text-blue-200">Home</NuxtLink>
          <NuxtLink to="/about" class="text-white hover:text-blue-200">About</NuxtLink>
          <NuxtLink to="/services" class="text-white hover:text-blue-200">Services</NuxtLink>
          <NuxtLink to="/contact" class="text-white hover:text-blue-200">Contact</NuxtLink>
        </div>
        <button @click="isMenuOpen = !isMenuOpen" class="md:hidden text-white focus:outline-none">
          <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
          </svg>
        </button>
      </div>
      <div v-if="isMenuOpen" class="md:hidden mt-2">
        <NuxtLink to="/" class="block text-white py-2">Home</NuxtLink>
        <NuxtLink to="/about" class="block text-white py-2">About</NuxtLink>
        <NuxtLink to="/services" class="block text-white py-2">Services</NuxtLink>
        <NuxtLink to="/contact" class="block text-white py-2">Contact</NuxtLink>
      </div>
    </nav>

    <!-- Main Content -->
<div  class="grid grid-cols-2 ">
  <div class="flex items-center pl-8 text-[20px] font-bold">
    <h4>Revolutionized medicine, developing life-saving drugs, vaccines, and treatments that have extended and improved countless lives.</h4>
  </div>
  <div class="pl-20">
    <img src="~/assets/images/bg2.png" alt="" class="">
  </div>
</div>

 <!-- Services Section -->
 <section class="bg-gray-100 py-16">
  <div class="container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center text-gray-800 mb-8">Our Medical Services</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <div v-for="service in services" :key="service.id" class="bg-white rounded-lg shadow-md overflow-hidden">
        <img :src="service.image" :alt="service.name" class="w-full h-48 object-cover">
        <div class="p-6">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">{{ service.name }}</h3>
          <p class="text-gray-600 mb-4">{{ service.description }}</p>
          <button @click="openModal(service)" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition duration-300">
            Learn More
          </button>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Modal -->
<div v-if="selectedService" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
  <div class="bg-white rounded-lg p-8 max-w-2xl w-full">
    <h2 class="text-2xl font-bold mb-4">{{ selectedService.name }}</h2>
    <img :src="selectedService.image" :alt="selectedService.name" class="w-full h-64 object-cover mb-4 rounded">
    <p class="text-gray-700 mb-4">{{ selectedService.fullDescription }}</p>
    <ul class="list-disc list-inside mb-4">
      <li v-for="feature in selectedService.keyFeatures" :key="feature" class="text-gray-600">
        {{ feature }}
      </li>
    </ul>
    <button @click="closeModal" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition duration-300">
      Close
    </button>
  </div>
</div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isMenuOpen = ref(false)


const services = ref([
  {
    id: 1,
    name: 'Advanced Diagnostics',
    description: 'Cutting-edge diagnostic technologies for accurate and timely results.',
    image: 'https://images.unsplash.com/photo-1576091160399-112ba8d25d1d?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    fullDescription: 'Our advanced diagnostics service utilizes state-of-the-art technology to provide precise and rapid results. From molecular testing to advanced imaging, we offer a comprehensive suite of diagnostic tools to aid in early detection and treatment planning.',
    keyFeatures: [
      'High-resolution imaging',
      'Molecular and genetic testing',
      'Rapid results delivery',
      'Integration with electronic health records'
    ]
  },
  {
    id: 2,
    name: 'Personalized Treatment Plans',
    description: 'Tailored medical approaches based on individual patient needs and genetic profiles.',
    image: 'https://images.unsplash.com/photo-1630959302862-173b63baa6a4?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    fullDescription: 'Our personalized treatment plans leverage the latest in genetic profiling and AI-driven analysis to create uniquely tailored medical approaches. We consider each patients individual characteristics, lifestyle, and preferences to design the most effective treatment strategy.',
    keyFeatures: [
      'Genetic profiling',
      'AI-assisted treatment design',
      'Ongoing plan adjustment',
      'Holistic health consideration'
    ]
  },
  {
    id: 3,
    name: 'Telemedicine Consultations',
    description: 'Remote medical consultations with experienced healthcare professionals.',
    image: 'https://images.unsplash.com/photo-1576091160550-2173dba999ef?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80',
    fullDescription: 'Our telemedicine consultations provide convenient access to top-tier medical expertise from the comfort of your home. Using secure video conferencing technology, patients can consult with specialists, receive diagnoses, and get prescriptions without the need for in-person visits.',
    keyFeatures: [
      'Secure video consultations',
      'Access to specialists',
      'Electronic prescriptions',
      'Follow-up care coordination'
    ]
  }
])

const selectedService = ref(null)

function openModal(service) {
  selectedService.value = service
}

function closeModal() {
  selectedService.value = null
}
</script>

<style>
/* Add any additional styles you need here */
</style>