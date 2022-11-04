<script setup>
  import { RouterLink } from 'vue-router';
</script>

<template>
  <section id="header">
    <!-- Logo -->
    <h1><RouterLink :to="{ name: 'home' }">AmiiVue</RouterLink></h1>
    <!-- Nav -->
    <nav id="nav">
      <ul>
        <li >
          <RouterLink :to="{ name: 'home' }">Home</RouterLink>
        </li>
        <!-- <li><a href="left-sidebar.html">Pokémons</a></li> -->
        <li >
          <RouterLink :to="{ name: 'list' }">Liste Amiibo</RouterLink>
        </li>
      </ul>
    </nav>
  </section>
</template>