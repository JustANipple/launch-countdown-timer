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

let currentTimeFormatted = ref(props.time);

let nextTimeFormatted = ref(props.time - 1);

const isFlipping = ref(false);

watch(
    () => props.time,
    (newTime) => {
        isFlipping.value = true;
        setTimeout(() => {
            isFlipping.value = false;
            currentTimeFormatted.value = String(newTime).padStart(2, "0");
            nextTimeFormatted.value = String(newTime - 1).padStart(2, "0");
        }, 495);
    },
);
</script>

<template>
    <div class="relative grid gap-y-10">
        <!-- Flipping Card -->
        <div
            class="relative z-10 grid h-[36px] w-[70px] origin-bottom text-4xl perspective-midrange transform-3d"
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

        <!-- Card -->
        <div class="absolute z-0 grid h-[36px] w-[70px] origin-bottom text-4xl">
            <!-- Upper -->
            <div
                class="h-[36px] overflow-hidden rounded-md bg-[#2b2d46] text-center"
            >
                <p class="translate-y-[50%] leading-none text-[#d75476]">
                    {{ nextTimeFormatted }}
                </p>
            </div>

            <!-- Lower -->
            <div
                class="h-[36px] overflow-hidden rounded-md bg-[#35364b] text-center"
            >
                <p class="-translate-y-[50%] leading-none text-[#fa6288]">
                    {{ currentTimeFormatted }}
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
    animation: flip 0.99s ease-in-out;
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
