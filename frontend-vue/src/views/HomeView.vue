<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <div
    class="relative flex w-screen h-full items-center justify-center bg-gradient-to-r from-[#292311] to-[#d19c49]"
  >
    <h1
      class="absolute z-10 w-full left-2.5 top-5 p-5 text-2xl text-[#f5af47] [text-shadow:3px_3px_0px_rgba(0,0,0,0.3),0px_0px_20px_#1b170f] sm:w-auto sm:left-[250px] sm:top-[150px] sm:p-0 sm:text-[4rem]"
    >
      Oli di Sicilia
    </h1>

    <RouterLink to="/prodotti">
      <h2
        class="absolute left-2.5 top-[250px] text-white text-2xl no-underline [text-shadow:3px_3px_3px_black] sm:left-[260px] sm:text-[2.2rem]"
      >
        Scopri i nostri prodotti
        <font-awesome-icon
          icon="arrow-right-to-bracket"
          class="block ml-[50%] text-2xl [filter:drop-shadow(2px_2px_4px_rgb(0,0,0))] sm:text-[2rem]"
        />
      </h2>
    </RouterLink>

    <!-- <img :src="'/images/hero-olive-v2.jpg'" alt="" /> -->
    <picture class="block">
      <!-- Mobile: Show a cropped portrait version -->
      <source media="(max-width: 600px)" srcset="/images/hero-olive-v2-smartphone.jpg" />
      <!-- Tablet: Show a medium version -->
      <source media="(max-width: 1024px)" srcset="/images/hero-olive-v2-tablet.jpg" />
      <!-- Desktop: Show the full wide version -->
      <img :src="'/images/hero-olive-v2.jpg'" alt="" />
    </picture>
  </div>
</template>