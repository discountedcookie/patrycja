<script setup lang="ts">
import ShapeLine from '@/components/ShapeLine.vue'

const word = 'pasozyt'
</script>

<template>
  <main>
    <div class="h-screen w-screen flex items-center justify-center">
      <ShapeLine
        :letter="letter"
        v-for="letter in word"
        :key="letter"
        class="absolute inset-0"
        :style="{
          transform: `rotate(${Math.random()*Math.PI*360}deg)`,
        }"
      />
    </div>
  </main>
</template>
