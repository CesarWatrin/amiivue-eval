<script setup>
import Header from '../components/Header.vue'
import Footer from "../components/Footer.vue";
</script>

<template>
  <div class="left-sidebar is-preload">
    <div id="page-wrapper">
      <Header />
      <slot />
      <Footer />
    </div>
  </div>
</template>