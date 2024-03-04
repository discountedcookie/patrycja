<script setup lang="ts">
import { onMounted } from 'vue';
import { RouterView } from 'vue-router'

onMounted(() => {
  document.documentElement.requestFullscreen()
})
</script>

<template>
  <RouterView />
</template>

