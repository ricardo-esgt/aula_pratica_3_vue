<script setup>
import { ref } from 'vue';
import axios from 'axios';

axios.defaults.withCredentials = true;
axios.defaults.withXSRFToken = true;

const name = ref("");

const email = ref("");

const password = ref("");

const passwordConfirmation = ref("");

const qrcode = ref("");

function submit() {

  let params = {
    name: name.value,
    email: email.value,
    password: password.value,
    password_confirmation: passwordConfirmation.value
  }

  axios.post("http://backend.aula-pratica.test/api/register", params)
    .then(({data}) => {
      qrcode.value = data.qrcode;
    })
}

</script>

<template>
  <main>
    <form @submit.prevent="submit">
      <div>
        <label>Name</label>
        <input type="text" required v-model="name">
      </div>
      <div>
        <label>Email</label>
        <input type="email" required v-model="email">
      </div>
      <div>
        <label>Password</label>
        <input type="password" required v-model="password">
      </div>
      <div>
        <label>Password Confirmation</label>
        <input type="password" required v-model="passwordConfirmation">
      </div>
      <button>Register</button>
    </form>

    <div v-html="qrcode" v-if="qrcode"></div>
  </main>
</template>
