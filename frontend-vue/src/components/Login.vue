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


<template>
  <div id="container" class="w-screen h-screen flex items-center justify-start">
    <LoadingSpinner v-if="loading" id="spinner" class="absolute" />
    <form class="max-w-100 min-w-75  mt-0 flex flex-col">
      <label for="username" class="text-2xl text-amber-100">Username</label>
      <input
        id="username"
        type="text"
        placeholder="Username"
        v-model="username"
        class="p-2 rounded-lg mb-5 bg-amber-100"
      />
      <label for="password" class="text-2xl text-amber-100">Password</label>
      <input
        id="password"
        type="password"
        placeholder="Password"
        v-model="password"
        class="p-2 rounded-lg mb-5 bg-amber-100"
      />
      <Button type="submit" @click.prevent="handleLogin"><span>Login</span></Button>
      <p v-if="error" class="text-2xl my-5 mx-auto text-red-600">{{ error }}</p>
      <p v-else class="text-2xl my-5 mx-auto text-green-600">{{ successMessage }}</p>
    </form>
  </div>
</template>