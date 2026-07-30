<script setup>
import { ref, reactive } from 'vue'
import { useAuthStore } from '@/stores/authStore'
import { useRouter } from 'vue-router'
import  Button  from '@/components/ui/Button.vue'


const authStore = useAuthStore()
const router = useRouter()

const form = reactive({
  username: '',
  email: '',
  first_name: '',
  last_name: '',
  password: '',
  password2: '',
})


const registrationMessage = ref('')
const registrationError = ref('')
const loading = ref(false)
const errors = reactive({
  username: '',
  email: '',
  password: '',
  password2: '',
})

// New registration function with DRF
const HandleRegister = async () => {
  registrationMessage.value = ''
  registrationError.value = ''
  Object.keys(errors).forEach((key) => (errors[key] = ''))

  loading.value = true

  const result = await authStore.register(form)

  if (result.success) {
    registrationMessage.value = 'Registration successful! Reindirizzamento al login...'
    // Clear form
    Object.keys(form).forEach((key) => (form[key] = ''))
    // Redirect to login after 2 sec
    setTimeout(() => {
      router.push('/login')
    }, 2000)
  } else {
    //Parse error message
    const errorText = result.error
    if (errorText.includes('username')) {
      errors.username = 'Username already exists or is invalid'
    } else if (errorText.includes('password')) {
      errors.password = 'Password does not meet requirements'
      errors.password2 = 'Password does not meet requirements'
    } else {
      registrationError.value = errorText || 'Registration failed. Please try again-'
    }
  }
  loading.value = false

}
</script>

<template>
  <form>
    <label for="nome">Nome</label>
    <input id="nome" type="text" placeholder="nome..." v-model="form.first_name" />
    <label for="cognome">Cognome</label>
    <input id="cognome" type="text" placeholder="Cognome..." v-model="form.last_name" />
    <label for="email">Email</label>
    <input type="email" placeholder="Email..." v-model="form.email" />
    <label for="username">Username</label>
    <input id="username" type="text" placeholder="Username..." v-model="form.username" />
    <label for="password">Password</label>
    <input id="password" type="password" placeholder="Password..." v-model="form.password" />
    <label for="password2">Conferma password</label>
    <input id="password2" type="password" placeholder="Reinserisci password..." v-model="form.password2" />
    <Button type='submit' @click.prevent="HandleRegister">Register</Button>
    <p v-if="registrationMessage" class="para success">{{ registrationMessage }}</p>
    <p v-else calss="para error">{{ registrationError }}</p>
  </form>
</template>

<style scoped>
form {
  margin-top: 0;
  max-width: 400px;
  min-width: 300px; 
  background-color: transparent;
}

label {
  font-size: 1rem;
}

input {
  padding: 8px;
  border-radius: 5px;
  margin-bottom: 10px;
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