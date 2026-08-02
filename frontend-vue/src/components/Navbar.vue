<script setup>
import { useAuthStore } from '@/stores/authStore'
import { useRouter } from 'vue-router'
import { useCartStore } from '@/stores/cartStore'
import { useTheme } from '@/composable/useTheme'

const router = useRouter()
const authStore = useAuthStore()
const cartStore = useCartStore()
const { isDark, toggleTheme } = useTheme()

function handleLogout() {
  authStore.logout()
  router.push('/login')
}
</script>

<template>
  <nav class="z-10 sticky top-0 bg-surface-2 
  border-border-light flex justify-evenly text-text-secondary 
  p-6 text-2xl">
    <!-- Logo del sito -->
    <div class="w-full font-bold">BrandLogo</div>
    <!-- Link di navigazione -->
    <ul class="flex w-full gap-6 whitespace-nowrap">
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/prodotti">Prodotti</router-link></li>
      <li class="no-wrap"><router-link to="/libri">Libri🔒</router-link></li>
      <li><router-link to="/users">Utenti🔒</router-link></li>
      <li v-if="authStore.token">
        <a href="#" @click.prevent="handleLogout">Logout</a>
      </li>
      <li v-else><router-link to="/login">Login</router-link></li>
      <li v-if="!authStore.isAuthenticated"><router-link to="/register">Register</router-link></li>
      <li class="relative">
        <router-link to="/cart"
          ><font-awesome-icon :icon="['fas', 'cart-shopping']" />
          <div
            class="absolute -top-4 -right-4 flex justify-center 
            items-center bg-red-500 w-6 h-6 rounded-full"
          >
            <span class="">{{ cartStore.totalItems }}</span>
          </div></router-link
        >
      </li>
      <li>
        <button @click="toggleTheme"><font-awesome-icon :icon="['fas', 'fa-sun']" v-if="isDark" 
          class="text-foreground" />
        <font-awesome-icon :icon="['fas', 'fa-moon']" v-else class="text-foreground" />
        </button>
      </li>
    </ul>
  </nav>
</template>


<style scoped>
li:hover {
  color: var(--color-text-inverted);
}

</style>
