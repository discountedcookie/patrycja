<script setup lang="ts">
import ShapeLine from '@/components/ShapeLine.vue'
import { ref } from 'vue'

const word = 'pasożyt'
const splitWord = ref(word.split('').reverse().join(''))
const letters = ref([] as string[])

function onClick(letter: string) {
  setTimeout(() => {
    letters.value.push(letter)
  }, 2400)
}
</script>

<template>
  <main class="h-screen w-screen">
    <div class="h-full w-full flex items-center justify-center">
      <ShapeLine
        :letter="letter"
        v-for="letter in splitWord"
        :key="letter"
        class="absolute inset-0 mx-auto w-2/3 h-2/3"
        :style="{
          transform: `rotate(${Math.random()*Math.PI*360}deg)`,
        }"
        @click="onClick(letter)"
      />
    </div>

    <div class="fixed bottom-10 inset-x-0 flex justify-center gap-2">
      <div v-for="(letter, index) in word" :key="letter" class="border rounded p-4">
        <p v-if="index < letters.length">
          {{ letter }}
        </p>

      </div>
    </div>
  </main>
</template>
