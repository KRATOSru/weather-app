<template>
  <div class="flex flex-col min-h-screen font-Roboto bg-weather-primary">
    <site-navigation />
    <h1>Hello App!</h1>
    <RouterView />
  </div>
</template>

<script setup>
import {RouterView} from 'vue-router'
import SiteNavigation from './components/SiteNavigation.vue'
</script>

<style lang="scss" scoped></style>
