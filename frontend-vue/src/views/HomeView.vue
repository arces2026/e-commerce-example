<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <div class="container">
    <h1>Oli di Sicilia</h1>
    <RouterLink to="/prodotti"
      ><h2>
        Scopri i nostri prodotti
        <font-awesome-icon icon="arrow-right-to-bracket" class="icon" /></h2
    ></RouterLink>
    <!-- <img :src="'/images/hero-olive-v2.jpg'" alt="" /> -->
    <picture class="image">
      <!-- Mobile: Show a cropped portrait version -->
      <source media="(max-width: 600px)" srcset="/images/hero-olive-v2-smartphone.jpg" />
      <!-- Tablet: Show a medium version -->
      <source media="(max-width: 1024px)" srcset="/images/hero-olive-v2-tablet.jpg" />
      <!-- Desktop: Show the full wide version -->
      <img :src="'/images/hero-olive-v2.jpg'" alt="" />
    </picture>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100%;
  background: linear-gradient(to right, #292311, #d19c49);
}

h1 {
  position: absolute;
  top: 150px;
  left: 250px;
  color: #f5af47;
  font-size: 4rem;
  text-shadow:
    3px 3px 0px rgba(0, 0, 0, 0.3),
    /* Deep shadow */ 0px 0px 20px #1b170f; /* Red glow on top */
  z-index: 10;
}

.icon {
  display: block;
  margin-left: 50%;
  font-size: 2rem;
  filter: drop-shadow(2px 2px 4px rgb(0, 0, 0));
}

h2 {
  position: absolute;
  top: 250px;
  left: 260px;
  text-decoration: none;
  color: white;
  font-size: 2.2rem;
  text-shadow: 3px 3px 3px black;
}

img {
  /* object-fit: fill; */
  /* border-radius: 50%; */
  /* height: 80vh; */
  /* mask-image: radial-gradient(circle, black 90%, transparent 100%);
  -webkit-mask-image: radial-gradient(circle, black 20%, transparent 100%); */
}

/* Smartphone styles (applies when screen is 768px or smaller) */
@media (max-width: 600px) {
  h1 {
    font-size: 2rem;
    padding: 20px;
    width: 100%;
    left: 10px;
  }

  h2 {
    font-size: 1.5rem;
    left: 10px;
  }

  .icon {
    font-size: 1.5rem;
  }
}
</style>
