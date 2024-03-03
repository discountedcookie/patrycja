<script lang="ts" setup>
import { SVG } from '@svgdotjs/svg.js';
import { onMounted, ref } from 'vue';

const canvas = ref()
const svg = ref()

const start = [6, 142];
const finish = [294, 143];

const path = `M${start[0]},${start[1]} Q 21,157 40,156 Q 60,151 75,140 Q 97,129 120,139 Q 143,145 169,151 Q 180,157 190,147 Q 203,141 209,147 Q 223,148 229,148 Q 240,147 247,142 Q 257,139 261,132 Q 269,119 277,132 Q 284,141 ${finish[0]},${finish[1]}`

onMounted(() => {
    svg.value = SVG().viewbox(0, 90, 300, 100).addTo(canvas.value)

    const route = svg.value
        .path(path)
        .fill('none')
        .stroke({ color: '#f06', width: 4, linecap: 'round', linejoin: 'round' })
})
</script>

<template>
    <div ref="canvas" />
</template>
