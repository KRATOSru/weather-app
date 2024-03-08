<template>
  <div>
    <Suspense>
      <AsyncCityView />
      <template #fallback>
        <p>Загружается....</p>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from '../components/AsyncCityView.vue'
</script>
