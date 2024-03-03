<script lang="ts" setup>
import anime, { type AnimeInstance } from 'animejs';
import * as R from 'radash';
import { computed, onMounted, ref, type StyleValue } from 'vue';

const props = defineProps<{ index: number, text: string, style: { transform: string } }>()

const el = ref()
const elClicked = ref(false)
const pathId = `path-${Math.random()}`;
const path = computed(() => `#${pathId}`);

const styleValue = computed(() => {
    if (elClicked.value) {
        return {
            content: `${props.style}`,
            transform: props.style.transform.replace(/translate\(.+\)/, 'translate(0, 0)')
        }
    } else {
        return props.style
    }
})
const breatheAnimation = ref<AnimeInstance>()

function onClick() {
    elClicked.value = true;

    breatheAnimation.value?.pause()
    breatheAnimation.value?.seek(0)

    anime({
        targets: el.value,
        rotate: 360,
        duration: 20000 + Math.random() * 5000,
        elasticity: 0,
        easing: 'linear',
        loop: true,
    })
}

onMounted(() => {
    breatheAnimation.value = anime({
        targets: el.value,
        scale: [1.025, 0.975],
        direction: 'alternate',
        easing: 'linear',
        duration: 750 + Math.random() * 500,
        loop: true,
    });
})
</script>

<template>
    <div class="absolute inset-x-0 origin-center active:z-10 transition-transform duration-[3s]" :style="styleValue"
        :class="{
        'pointer-events-none': elClicked
    }">
        <svg viewBox="0 0 1000 1000" ref="el" class="group" @click="onClick"
            :style="{ scale: 1 - Math.sin(0.09 * index) }">
            <path :id="pathId" d="M 0 500 m -0 0 a 1,1 0 1,0 1000,0 a 1,1 0 1,0 -1000,0" fill="transparent"
                :class="{ 'group-active:fill-red-500': !elClicked }" />

            <text text-anchor="middle" dy="-0.2em" font-size="72px" x="85%">
                <textPath :href="path">
                    {{ text }}
                </textPath>
            </text>
        </svg>
    </div>
</template>