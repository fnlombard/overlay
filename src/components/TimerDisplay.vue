<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const elapsed_time = ref(0);
const timeLeft = ref(0);
const taskTime = ref(15);
const step = ref(1);

const formattedTime = computed(() => {
    let minutes = Math.floor(timeLeft.value / 60);
    let seconds = Math.floor(timeLeft.value % 60);
    return `${minutes < 10 ? '0' + minutes : minutes}:${seconds < 10 ? '0' + seconds : seconds}`;
});

let intervalId = setInterval(() => {
    elapsed_time.value += 1;
    timeLeft.value = taskTime.value * 60 - elapsed_time.value;
    if (timeLeft.value < 0) {
        timeLeft.value = 0;
    }
}, 1000);

onUnmounted(() => {
    if (intervalId) {
        clearInterval(intervalId);
    }
});

</script>


<template>
    <div class="timer">
        {{ formattedTime }}
    </div>
</template>

<style scoped>
.timer {
    font-size: 24px;
}
</style>
