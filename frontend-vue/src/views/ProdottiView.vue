<script setup>
import { onMounted, ref } from 'vue'
import ProductCard from '@/components/ProductCard.vue'
import { useCartStore } from '@/stores/cartStore'
import { get } from '@/plugins/api'
import LoadingSpinner from '@/components/LoadingSpinner.vue'


const cartStore = useCartStore()

console.log({ cart: cartStore.totalItems })


const products = ref([])
const error = ref(null)
const loading = ref(false)

onMounted(async () => {
  try {
    // products.value = await getProducts()
    loading.value = true
    const token = localStorage.getItem('access_token')
    const data = await get('/api/v1/scarpe', {
      Authorization: `Bearer ${token}`,
    })
    loading.value = false
    console.log({ dataresults: data.results })
    products.value = data.results
  } catch (err) {
    error.value = 'Impossibile caricare i prodotti.'
  } finally {
    loading.value = false
  }
  // console.log(products.value)
})
</script>

<template>

  <div id="container">
     
  <h1>Lista prodotti</h1>
  <main class="grid">
     <LoadingSpinner v-if="loading" class="spinner"/>
    <ProductCard v-for="product in products" :key="product.id">
      <template #image>
        <div class="badge-wrapper">
          <span v-if="product.sconto" class="badge">sconto {{ product.sconto }} %</span>
          <router-link :to="`/detail/${product.id}`">
            <img :src="product.immagine_url" :alt="product.nome" />
          </router-link>
        </div>
      </template>

      <template #content>
        <router-link :to="`/detail/${product.id}`" id="r-link-content">
          <span class="category">{{ product.categoria }}</span>
          <h3 class="custom-title">{{ product.nome }}</h3>
          <p class="custom-desc">
            {{ product.descrizione }}
          </p>
        </router-link>
      </template>

      <template #footer>
        <div class="price-container">
          <span class="old-price">€ {{ product.prezzo }}</span>
          <span class="new-price">€ {{ product.prezzo_scontato.toFixed(2) }}</span>
        </div>
        <button class="add-btn" @click="cartStore.addToCart">Aggiungi</button>
      </template>
    </ProductCard>
  </main>
  </div>
</template>

<style scoped>
#container {
 /* background: linear-gradient(to right, #292311, #d19c49); */
}

.spinner {
  position: absolute;
  top: 50%;
  left: 50%;
}

h1 {
  text-align: center;
  font-size: 3.5rem;
  /* color:#c9974d; */
  color: white;
  /* text-shadow: 3px 3px 6px; */
  text-shadow: 3px 3px 0px rgba(0, 0, 0, 0.3),
    /* Deep shadow */ 0px 0px 20px #5c5038; /* Red glow on top */
}

h3 {
  color: #292311;
}

.grid {
   position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 30px;
  padding: 30px;
}

.badge {
  position: absolute;
  left: 10px;
  top: 10px;
  color: rgb(245, 229, 229);
  background-color: rgba(233, 7, 7, 0.671);
  border-radius: 7px;
  font-size: 0.8em;
  padding: 4px;
}
#r-link-content {
  text-decoration: none;
  color: inherit;
}
.add-btn {
  padding: 10px;
  cursor: pointer;
  border-radius: 7px;
}

.old-price {
  font-size: 0.9rem;
  color: #757575;
  /* Grigio sbiadito */
  text-decoration: line-through;
  /* Barra il testo */
  margin-right: 10px;
}

/* Stile per il nuovo prezzo */
.new-price {
  font-size: 1.25rem;
  font-weight: bold;
  color: #d32f2f;
  /* Un rosso per l'offerta, oppure usa il verde/colore del tuo brand */
}
</style>
