<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue'
import Navi from './components/Navi.vue';
</script>

<template>
  <v-app>
    <div>

    <Navi />
    <Header />
    </div>
    <v-main>
      <RouterView />
    </v-main>
  </v-app>
</template>