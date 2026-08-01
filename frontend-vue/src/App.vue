<script setup>
import Navbar from './components/Navbar.vue'
import FooterVue from './components/FooterVue.vue'
</script>

<template>
    <div class="flex flex-col min-h-screen">
  <Navbar />
  <main class="flex-1 flex flex-col">
    <RouterView />
  </main>
  <FooterVue />
  </div>
</template>
