<script setup>
  import {defineProps} from 'vue';
  import { useRouter } from 'vue-router';

  const router = useRouter();

  defineProps({
    amiibo: Object,
  });
</script>

<template>
  <div class="col-4 col-12-medium cursor-pointer" @click="router.push({ name: 'details', params: { id: amiibo.tail }})">
    <section class="middle">
      <img :src="amiibo.image" />
      <header>
        <h2>{{ amiibo.character }}</h2>
      </header>
      <p>{{ amiibo.gameSeries }}</p>
    </section>
  </div>
</template>