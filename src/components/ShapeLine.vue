<script setup lang="ts">
import { ref, watchEffect } from 'vue'

defineProps<{
  letter: string
}>()

const id = ref(`${Math.random()}`)
const visible = ref(true)

function onClick() {
  setTimeout(() => {
    visible.value = false
  }, 2400)
}

const randomMinMax = (min: number, max: number) => Math.floor(Math.random() * (max - min + 1) + min)
const d = ref(`M ${randomMinMax(10, 20)} ${randomMinMax(10, 20)} C ${randomMinMax(30, 70)} ${randomMinMax(20, 80)} ${randomMinMax(10, 90)} ${randomMinMax(40, 60)} ${randomMinMax(50, 80)} ${randomMinMax(60, 70)} ${randomMinMax(80, 90)} ${randomMinMax(80, 90)}`)
</script>

<template>
  <svg viewBox="0 0 100 100" v-if="visible">
    <path
      :id="id"
      :d="d"
      class="fill-transparent stroke-red-500"
    />

    <text>
      <textPath class="hover:fill-green-500" :href="`#${id}`" startOffset="0%" @click="onClick">
        <animate attributeName="startOffset" fill="freeze" from="0%" to="150%" begin="click" dur="3s"></animate>

        {{ letter.repeat(20) }}
      </textPath>
    </text>
  </svg>
</template>

<style scoped>

</style>
