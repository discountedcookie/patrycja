<script setup lang="ts">
import anime from 'animejs';
import * as R from 'radash';
import { SVG } from '@svgdotjs/svg.js';
import { onMounted, ref } from 'vue';

const circles = [
    'lorem ipsum dolor sit amet',
    'consectetur adipisicing elit',
    'minima facilis doloribus quo est nesciunt',
    'assumenda aliquid earum esse libero voluptatem',
    'exercitationem nobis',
    'inventore aspernatur ad voluptate',
    'dolorem eius ex facilis',
]
const container = ref()

function randomFloat(min: number, max: number, randomNegative: boolean = false) {
    const rand = Math.random() * (max - min + 1) + min
    return randomNegative ? rand * (Math.round(Math.random()) ? 1 : -1) : rand
}

onMounted(() => {
    circles.reverse().forEach((circle, index) => {
        const el = document.createElement('div')
        el.className = 'absolute'
        el.style.scale = randomFloat(0.9, 1.1).toString()
        el.style.transform = `translate(${randomFloat(20, 40, true)}%, ${randomFloat(20, 40, true)}%)`

        container.value.appendChild(el)

        const svg = SVG().size(320, 320)
            .addClass('group')
            .addTo(el)

        const path = svg.path('M 110 160 m -100 0 a 150,150 0 1,0 300,0 a 150,150 0 1,0 -300,0')
            .scale(1 - 0.1 * index)
            .fill('transparent')
            .addClass('group-hover:fill-red-500')
            .click(() => {
                breatheAnimation.reset()
                rotatingAnimation.play()

                el.classList.add('pointer-events-none')
                el.style.scale = '1'
                el.style.transform = ''
            })

        const text = svg.textPath(circle, path)
            .attr('text-anchor', 'start')
            .attr('side', 'right')

        const breatheAnimation = anime({
            targets: svg.node,
            scale: [1, 1.05],
            duration: 750,
            direction: 'alternate',
            loop: true,
            when: 'now',
            easing: 'linear'
        })

        const rotatingAnimation = anime({
            targets: svg.node,
            rotate: 360,
            duration: 10000 + 5000 * Math.random(),
            elasticity: 0,
            easing: 'linear',
            loop: true,
            delay: anime.stagger(1000)
        })
        rotatingAnimation.pause()
    })
})
</script>

<template>
    <div ref="container"
        class="h-screen w-screen bg-black fill-white overflow-hidden flex items-center justify-center" />
</template>
