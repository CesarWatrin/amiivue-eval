<script setup>
  import {onMounted, ref} from "vue";
  import axios from "axios";
  import { useRoute } from 'vue-router';

  const route = useRoute();
  const amiiboId = route.params.id;
  const currentAmiibo = ref({});
  const isLoading = ref(true);

  onMounted(async () => {
    const movie = await axios.get('https://www.amiiboapi.com/api/amiibo/?tail=' + amiiboId);
    const { status, data } = movie;

    if (status === 200) {
      currentAmiibo.value = data.amiibo[0];
      isLoading.value = false;
    }
  });
</script>

<template>
  <section id="main">
    <div class="container">
      <div v-if="!isLoading" class="row">
        <div class="col-4 col-12-medium">
          <!-- Sidebar -->
          <section class="box">
            <header>
              <h3>Infos</h3>
            </header>
            <p> amiiboSeries: <b>{{ currentAmiibo.amiiboSeries }}</b> <br />
              character: <b>{{ currentAmiibo.character }}</b><br />
              gameSeries: <b>{{ currentAmiibo.gameSeries }}</b><br />
              type: <b>{{ currentAmiibo.type }}</b>
            </p>
          </section>
          <section class="box">
            <header>
              <h3>Dates sorties</h3>
            </header>
            <ul class="divided">
              <li v-for="(release, key) in currentAmiibo.release" :key="key">
                <b>{{ key }}</b> : {{ release }}
              </li>
            </ul>
          </section>
        </div>
        <div class="col-8 col-12-medium imp-medium">
          <!-- Content -->
          <article class="box post">
            <img :src="currentAmiibo.image" alt="" />
            <header>
              <h2>{{ currentAmiibo.character }}</h2>
              <p>{{ currentAmiibo.type }}</p>
            </header>
          </article>
        </div>
      </div>
      <div v-else class="row">
        <p>Chargement...</p>
      </div>
    </div>
  </section>
</template>