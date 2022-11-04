<script setup>
  import axios from 'axios';
  import { useRouter } from 'vue-router';
  import {onMounted, ref} from "vue";

  const router = useRouter();

  const allAmiibos = ref([]);
  const isLoading = ref(true);

  onMounted(async () => {
    const amiibos = await axios.get('https://www.amiiboapi.com/api/amiibo/');
    const { status, data } = amiibos;

    if (status === 200) {
      allAmiibos.value = data.amiibo;
      isLoading.value = false;
    }
  });
</script>

<template>
  <section id="main">
    <div class="container">
      <!-- Content -->
      <article class="box post">
        <header>
          <h2>Ma Collection</h2>
          <p>{{ allAmiibos.length }}</p>
        </header>
        <table>
          <tr>
            <th>Character</th>
            <th>game Series</th>
            <th>Action</th>
          </tr>
          <template v-if="!isLoading">
            <tr v-for="amiibo in allAmiibos" :key="amiibo.tail">
              <td>{{ amiibo.character }}</td>
              <td>{{ amiibo.gameSeries }}</td>
              <td>
                <button @click="router.push({ name: 'details', params: { id: amiibo.tail }})">voir</button>
              </td>
            </tr>
          </template>
          <template v-else>
            <tr>
              <td colspan="3">Chargement...</td>
            </tr>
          </template>
        </table>
      </article>
    </div>
  </section>
</template>
