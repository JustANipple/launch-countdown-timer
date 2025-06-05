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

const currentTimeFormatted = computed(() => {
    return String(props.time).padStart(2, "0");
});

const nextTimeFormatted = computed(() => {
    return String(props.time - 1).padStart(2, "0");
});

const isFlipping = ref(false);

watch(
    () => props.time,
    () => {
        isFlipping.value = true;
        setTimeout(() => {
            isFlipping.value = false;
        }, 3000);
    },
);
</script>

<template>
    <!-- Container -->
    <div class="grid gap-y-4 transform-3d">
        <!-- Card : Front -->
        <div class="grid text-4xl">
            <!-- Half : Upper -->
            <div
                class="relative z-10 w-[70px] origin-bottom overflow-hidden rounded-md bg-[#2b2d46] text-center transform-3d"
                :class="{ 'animate-flip': isFlipping }"
            >
                <p class="translate-y-[50%] leading-none text-[#d75476]">
                    {{ currentTimeFormatted }}
                </p>
            </div>
            <!-- Half : Lower -->
            <div
                class="relative z-0 w-[70px] overflow-hidden rounded-md bg-[#35364b] text-center"
            >
                <p class="-translate-y-[50%] leading-none text-[#fa6288]">
                    {{ currentTimeFormatted }}
                </p>
            </div>
        </div>
        <!-- Card : Back -->
        <div class="grid text-4xl">
            <!-- Half : Upper -->
            <div
                class="w-[70px] overflow-hidden rounded-md bg-[#2b2d46] text-center"
            >
                <p class="translate-y-[50%] leading-none text-[#d75476]">
                    {{ nextTimeFormatted }}
                </p>
            </div>
            <!-- Half : Lower -->
            <div
                class="w-[70px] overflow-hidden rounded-md bg-[#35364b] text-center"
            >
                <p class="-translate-y-[50%] leading-none text-[#fa6288]">
                    {{ nextTimeFormatted }}
                </p>
            </div>
        </div>
        <p
            class="text-center text-[7px] font-thin tracking-[.25rem] text-white uppercase opacity-70"
        >
            {{ props.timeType }}
        </p>
    </div>
</template>

<style scoped>
.animate-flip {
    animation: flip 3s ease-in-out forwards;
}

@keyframes flip {
    0% {
        transform: rotateX(0deg);
    }
    50% {
        transform: rotateX(180deg);
    }
    100% {
        transform: rotateX(180deg);
    }
}
</style>
