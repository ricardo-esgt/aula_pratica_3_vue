<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router'

axios.defaults.withCredentials = true;
axios.defaults.withXSRFToken = true;

const email = ref("");

const password = ref("");

const correctCredentials = ref(false)

const otp = ref("");

const router = useRouter()

function login() {

  let params = {
    email: email.value,
    password: password.value,
  }

  axios.post("http://backend.aula-pratica.test/api/login", params)
    .then(() => {
     correctCredentials.value = true
    })
}

function login2FA() {

  let params = {
    code: otp.value,
  }

  axios.post("http://backend.aula-pratica.test/api/two-factor-challenge", params)
    .then(() => {
      router.push("/")
    })
}

</script>

<template>
  <main>
    <form @submit.prevent="login" v-if="!correctCredentials">
      <div>
        <label>Email</label>
        <input type="email" required v-model="email">
      </div>
      <div>
        <label>Password</label>
        <input type="password" required v-model="password">
      </div>
      <button>Login</button>
    </form>

    <form @submit.prevent="login2FA" v-else>
      <div>
        <label>OTP</label>
        <input type="text" required v-model="otp">
      </div>
      <button>Login</button>
    </form>
  </main>
</template>
