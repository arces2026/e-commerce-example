<script setup>
import { ref } from 'vue';
import Navbar from './components/Navbar.vue';
import FooterVue from './components/FooterVue.vue';
</script>

<template>
    <Navbar></Navbar>
    <main>
        <RouterView />
    </main>
    <FooterVue />
</template>

