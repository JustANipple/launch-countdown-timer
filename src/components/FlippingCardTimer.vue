<script setup>
import { computed, ref, watch } from "vue";

const props = defineProps({
    time: {
        type: Number,
        required: true,
    },
    timeType: {
        type: String,
        required: true,
    },
});

const currentTime = ref(props.time);
const nextTime = ref(props.time);

const currentTimeFormatted = computed(() => {
    return String(props.time).padStart(2, "0");
});

const nextTimeFormatted = computed(() => {
    return String(props.time - 1).padStart(2, "0");
});

const isFlipping = ref(false);

watch(
    () => props.time,
    (newTime) => {
        isFlipping.value = true;
        setTimeout(() => {
            isFlipping.value = false;
        }, 750);
    },
);
</script>

<template>
    <div class="grid gap-y-10">
        <!-- Flipping Card -->
        <div
            class="relative grid h-[36px] w-[70px] origin-bottom text-4xl perspective-midrange transform-3d"
            :class="{ 'animate-flip': isFlipping }"
        >
            <!-- Front face -->
            <div
                class="absolute inset-0 overflow-hidden rounded-md bg-[#2b2d46] text-center backface-hidden"
            >
                <p class="translate-y-[50%] leading-none text-[#d75476]">
                    {{ currentTimeFormatted }}
                </p>
            </div>

            <!-- Back face (flipped) -->
            <div
                class="absolute inset-0 rotate-x-180 overflow-hidden rounded-md bg-[#35364b] text-center backface-hidden"
            >
                <p class="-translate-y-[50%] leading-none text-[#fa6288]">
                    {{ nextTimeFormatted }}
                </p>
            </div>
        </div>

        <!-- Label -->
        <p
            class="text-center text-[7px] font-thin tracking-[.25rem] text-white uppercase opacity-70"
        >
            {{ props.timeType }}
        </p>
    </div>
</template>

<style scoped>
.animate-flip {
    animation: flip 0.75s ease-in-out;
}

@keyframes flip {
    0% {
        transform: rotateX(0deg);
    }
    50% {
        transform: rotateX(180deg);
    }
    100% {
        transform: rotateX(360deg);
    }
}
</style>
