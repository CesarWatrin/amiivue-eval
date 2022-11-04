<script setup>
  import axios from 'axios';
  import { RouterLink } from 'vue-router';
  import {onMounted, ref} from "vue";
  import Amiibo from '../components/Amiibo.vue';

  const allAmiibos = ref([]);
  const isLoading = ref(true);

  onMounted(async () => {
    const amiibos = await axios.get('https://www.amiiboapi.com/api/amiibo/');
    const { status, data } = amiibos;

    const randomNumber = Math.random() * (data.amiibo.length - 3);

    if (status === 200) {
      allAmiibos.value = data.amiibo.slice(randomNumber, randomNumber + 3);
      isLoading.value = false;
    }
  });
</script>

<template>
  <section id="home-main">
    <!-- Banner -->
    <section id="banner">
      <header>
        <h2>Hey.Bienvenue sur ma collection</h2>
      </header>
    </section>
    <!-- Intro -->
    <section id="intro" class="container">
      <div v-if="!isLoading" class="row">
        <Amiibo v-for="amiibo in allAmiibos" :key="amiibo.tail" :amiibo="amiibo"/>
      </div>
      <div v-else>
        <p class="loading">Chargement...</p>
      </div>
      <footer>
        <ul class="actions">
          <li>
            <RouterLink class="button large" :to="{ name: 'list' }">Liste complète</RouterLink>
          </li>
        </ul>
      </footer>
    </section>
  </section>
</template>
