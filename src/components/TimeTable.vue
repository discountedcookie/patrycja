<template>
    <div class="absolute grid grid-cols-3 gap-x-3 bg-gray-200 p-1 rounded border border-gray-500 leading-none"
        :style="timetable.pos">
        <div v-for="time in timetable.times.flat()" :key="`${timetable.id}-${time}`">
            <span class="text-sm">{{ time }}</span>
        </div>
    </div>
</template>