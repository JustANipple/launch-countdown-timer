<script setup>
import { ref } from "vue";
import FlippingCardTimer from "./components/FlippingCardTimer.vue";

const time = ref({
    days: 8,
    hours: 23,
    minutes: 55,
    seconds: 41,
});

setInterval(() => {
    handleSeconds(time.value);
}, 1000);

function handleSeconds(time) {
    if (time.seconds - 1 === 0) {
        time.seconds = 59;
        handleMinutes(time);
    } else {
        time.seconds -= 1;
    }
}

function handleMinutes(time) {
    if (time.minutes - 1 === 0) {
        time.minutes = 59;
        handleHours(time);
    } else {
        time.minutes -= 1;
    }
}

function handleHours(time) {
    if (time.hours - 1 === 0) {
        time.hours = 23;
        handleDays(time);
    } else {
        time.hours -= 1;
    }
}

function handleDays(time) {
    if (time.days - 1 === 0) {
        time.days = 0;
    } else {
        time.days -= 1;
    }
}
</script>

<template>
    <main class="bg-very-dark-blue-mostly-black flex min-h-screen flex-col">
        <div
            class="flex flex-1 items-center justify-center bg-[url(/images/bg-stars.svg)]"
        >
            <div class="grid gap-y-[60px]">
                <h1
                    class="text-center text-lg leading-6 font-semibold tracking-[0.375rem] text-white uppercase"
                >
                    We're launching <span class="block sm:inline">soon</span>
                </h1>
                <div class="flex gap-4">
                    <FlippingCardTimer :time="time.days" :timeType="'days'" />
                    <FlippingCardTimer :time="time.hours" :timeType="'hours'" />
                    <FlippingCardTimer
                        :time="time.minutes"
                        :timeType="'minutes'"
                    />
                    <FlippingCardTimer
                        :time="time.seconds"
                        :timeType="'seconds'"
                    />
                </div>
            </div>
        </div>
        <footer
            class="flex h-[168px] items-end justify-center bg-[url(/images/pattern-hills.svg)] bg-size-[950px_130px] bg-[position:calc(100%+4.75rem)_0] bg-no-repeat"
        >
            <div
                class="flex w-full items-center justify-center gap-8 bg-[#2f2439] pb-12"
            >
                <img src="/images/icon-facebook.svg" alt="" />
                <img src="/images/icon-pinterest.svg" alt="" />
                <img src="/images/icon-instagram.svg" alt="" />
            </div>
        </footer>
    </main>
</template>
