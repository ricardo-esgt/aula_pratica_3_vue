<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

axios.defaults.withCredentials = true;
axios.defaults.withXSRFToken = true;

const name = ref("");

const router = useRouter();

onMounted(() => {
  axios.get("http://backend.aula-pratica.test/api/user")
    .then(({data}) => {
      name.value = data.name;
    }).catch(() => {
      router.push("/login");
    })
})
</script>

<template>
  <main>
    <h1 v-if="name">Authenticated {{ name }}</h1>
  </main>
</template>
