<template>
  <v-app>
    <v-main class="main">
      <HomePageVue />
    </v-main>
  </v-app>
</template>

<script setup>
import HomePageVue from "./components/HomePage.vue";
</script>

<style scoped>
.main {
  background-color: #2c9e22;
}
</style>