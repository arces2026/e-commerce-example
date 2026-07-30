<script setup>
import { useAuthStore } from '@/stores/authStore'
import { useRouter } from 'vue-router'
import { useCartStore } from '@/stores/cartStore'

const router = useRouter()
const authStore = useAuthStore()
const cartStore = useCartStore()

function handleLogout() {
  authStore.logout()
  router.push('/login')
}
</script>

<template>
  <nav class="navbar">
    <!-- Logo del sito -->
    <div class="logo">BrandLogo</div>
    <!-- Link di navigazione -->
    <ul class="nav-links">
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/prodotti">Prodotti</router-link></li>
      <li><router-link to="/libri">Libri 🔒</router-link></li>
      <li><router-link to="/users">Utenti 🔒</router-link></li>
      <li v-if="authStore.token">
        <a href="#" @click.prevent="handleLogout">Logout</a>
      </li>
      <li v-else><router-link to="/login">Login</router-link></li>
      <li><router-link to="/register">Register</router-link></li>
      <li id="cart">
        <router-link to="/cart"
          ><font-awesome-icon :icon="['fas', 'cart-shopping']" /><div id='counter-container'><span id="counter">{{
            cartStore.totalItems
          }}</span></div></router-link
        >
      </li>
    </ul>
  </nav>
</template>



<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  /* border: 1px solid white; */
}

/* Stile principale della Navbar */
.navbar {
  display: flex;
  justify-content: space-between; /* Separa il logo dai link */
  align-items: center; /* Allinea verticalmente al centro */
  background-color: #1a1a1a; /* Colore di sfondo scuro */
  padding: 15px 30px;
  position: sticky; /* Mantiene la barra fissa in alto durante lo scroll */
  top: 0;
  z-index: 1000;
}

/* Stile del Logo */
.navbar .logo {
  color: #ffffff;
  font-size: 24px;
  font-weight: bold;
  letter-spacing: 1px;
}

/* Contenitore dei Link */
.navbar .nav-links {
  display: flex;
  list-style: none; /* Rimuove i pallini dell'elenco puntato */
}

/* Spaziatura tra i singoli elementi della lista */
.navbar .nav-links li {
  padding: 0 15px;
}

/* Stile dei singoli link ipertestuali */
.navbar .nav-links a {
  color: #e0e0e0;
  text-decoration: none; /* Rimuove la sottolineatura di default */
  font-size: 16px;
  font-weight: 500;
  transition: color 0.3s ease; /* Transizione fluida per l'effetto hover */
}

/* Effetto al passaggio del mouse (Hover) */
.navbar .nav-links a:hover {
  color: #4da6ff; /* Cambia colore quando l'utente ci passa sopra */
}

#cart {
    position: relative;
}
#counter-container {
    position: absolute;
    top: -8px;
    right: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: red;
    border-radius: 50%;
    width: 17px;
    font-size: .8rem;
}


/* 📱 Ottimizzazione Mobile (Responsive) */
@media screen and (max-width: 768px) {
  .navbar {
    flex-direction: column; /* Dispone logo e link in verticale su schermi piccoli */
    gap: 15px;
  }

  .navbar .nav-links {
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
  }

  .navbar .nav-links li {
    padding: 5px 10px;
  }
}
</style>
