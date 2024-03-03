<script setup lang="ts">
import anime from 'animejs';
import * as R from 'radash';
import { SVG } from '@svgdotjs/svg.js';
import { onMounted, ref } from 'vue';
import CircleText from './CircleText.vue';

const rotateDeg = (min: number, max: number) => `${R.random(min, max)}deg`
const translatePercent = (min: number, max: number) => `${R.random(min, max)}%`

const circles = [
    {
        text: 'lorem ipsum dolor sit amet',
        style: {
            transform: `rotate(${rotateDeg(50, 80)}) translate(${translatePercent(-40, -30)}, ${translatePercent(-70, -60)})`
        }
    },
    {
        text: 'consectetur adipisicing elit',
        style: {
            transform: `rotate(${rotateDeg(170, 190)}) translate(${translatePercent(-40, -30)}, ${translatePercent(-60, -50)})`,
        }
    },
    {
        text: 'minima facilis doloribus quo est nesciunt',
        style: {
            transform: `rotate(${rotateDeg(-50, -40)}) translate(${translatePercent(-10, 10)}, ${translatePercent(-60, -50)})`
        }
    },
    // {
    //     text: 'assumenda aliquid earum esse libero voluptatem',
    //     style: {
    //         transform: `rotate(${rotateDeg(0, 0)}) translate(${translatePercent(0, 0)}, ${translatePercent(0, 0)})`
    //     }
    // },
    // {
    //     text: 'exercitationem nobis',
    //     style: {
    //         transform: `rotate(${rotateDeg(0, 0)}) translate(${translatePercent(0, 0)}, ${translatePercent(0, 0)})`
    //     }
    // },
    // {
    //     text: 'inventore aspernatur ad voluptate',
    //     style: {
    //         transform: `rotate(${rotateDeg(0, 0)}) translate(${translatePercent(0, 0)}, ${translatePercent(0, 0)})`
    //     }
    // },
    // {
    //     text: 'dolorem eius ex facilis',
    //     style: {
    //         transform: `rotate(${rotateDeg(0, 0)}) translate(${translatePercent(0, 0)}, ${translatePercent(0, 0)})`
    //     }
    // }
]

// const rotatingAnimation = anime({
//     targets: '.circle',
//     rotate: 360,
//     duration: 10000 + Math.random() * 5000,
//     elasticity: 0,
//     easing: 'linear',
//     loop: true,
// })

// const container = ref()

// function randomFloat(min: number, max: number, randomNegative: boolean = false) {
//     const rand = Math.random() * (max - min + 1) + min
//     return randomNegative ? rand * (Math.round(Math.random()) ? 1 : -1) : rand
// }

// onMounted(() => {
//     circles.reverse().forEach((circle, index) => {
//         const el = document.createElement('div')
//         el.className = 'absolute'
//         el.style.scale = randomFloat(0.9, 1.1).toString()
//         el.style.transform = `translate(${randomFloat(20, 40, true)}%, ${randomFloat(20, 40, true)}%)`

//         container.value.appendChild(el)

//         const svg = SVG().size(320, 320)
//             .addClass('group')
//             .addTo(el)

//         const path = svg.path('M 110 160 m -100 0 a 150,150 0 1,0 300,0 a 150,150 0 1,0 -300,0')
//             .scale(1 - 0.1 * index)
//             .fill('transparent')
//             .addClass('group-hover:fill-red-500')
//             .click(() => {
//                 breatheAnimation.pause()
//                 breatheAnimation.seek(0)

//                 rotatingAnimation.play()

//                 el.classList.add('pointer-events-none')
//                 el.style.scale = '1'
//                 el.style.transform = ''
//             })

//         const text = svg.textPath(circle, path)
//             .attr('text-anchor', 'start')
//             .attr('side', 'right')

//         const breatheAnimation = anime({
//             targets: svg.node,
//             scale: [1, 1.05],
//             duration: 750,
//             direction: 'alternate',
//             loop: true,
//             when: 'now',
//             easing: 'linear'
//         })

//         const rotatingAnimation = anime({
//             targets: svg.node,
//             rotate: 360,
//             duration: 10000 + 5000 * Math.random(),
//             elasticity: 0,
//             easing: 'linear',
//             loop: true,
//             delay: anime.stagger(1000)
//         })
//         rotatingAnimation.pause()
//     })
// })
</script>

<template>
    <div class="bg-black fill-white h-screen w-screen flex items-center justify-center">
        <CircleText :index="index" :text="circle.text" :style="circle.style" v-for="(circle, index) in circles"
            :key="circle.text" />
    </div>

    <!-- <div ref="container"
        class="h-screen w-screen bg-black fill-white overflow-hidden flex items-center justify-center" /> -->
</template>
