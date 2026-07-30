<script setup>
import { ref } from 'vue'
import { useAuthStore } from '@/stores/authStore'
import { useRouter } from 'vue-router'
import Button from './ui/Button.vue'
import LoadingSpinner from './LoadingSpinner.vue'

const authStore = useAuthStore()
const router = useRouter()

const username = ref('')
const password = ref('')
const loading = ref(false)
const error = ref('')
const successMessage = ref('')

const handleLogin = async () => {
  loading.value = true
  error.value = ''

  const result = await authStore.login(username.value, password.value)

  if (result.success) {
    successMessage.value = 'Accesso effettuato con successo. Reindirizzamento...'
    setTimeout(() => {
      router.push('/')
    }, 2000)
  } else {
    error.value = 'Invalid username or password'
  }
  loading.value = false
}
</script>
e

<template>
  <div id="container">
    <LoadingSpinner v-if="loading" id="spinner" />
    <form>
      <label for="username">Username</label>
      <input id="username" type="text" placeholder="Username" v-model="username" />
      <label for="password">Password</label>
      <input id="password" type="password" placeholder="Password" v-model="password" />
      <Button type="submit" @click.prevent="handleLogin"> <span>Login</span> </Button>
      <p v-if="error" class="para error">{{ error }}</p>
      <p v-else class="para success">{{ successMessage }}</p>
    </form>
  </div>
</template>

<style scoped>
#container {
  width: 100vw;
  display: flex;
  align-items: start;
  justify-content: flex-start;
  height: 100vh;
}

#spinner {
  position: absolute;
}
form {
  max-width: 400px;
  min-width: 300px;
  background-color: transparent;
  margin-top: 0;
}

label {
  font-size: 1.5rem;
}

input {
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 20px;
}

.para {
  font-size: 1.5rem;
  margin: 20px auto;
}

.para.error {
  color: red;
}

.para.success {
  color: green;
}
</style>
