<script setup lang="ts">
import { computed, onUnmounted, ComputedRef, ref } from 'vue';

const props = defineProps<{
  task_time: number
}>();

const elapsed_time = ref<number>(0);

const formattedTime: ComputedRef<string> = computed(() => {
    let time_left: number = props.task_time - elapsed_time.value;
    time_left = time_left < 0 ? 0 : time_left;

    let minutes = Math.floor(time_left / 60);
    let seconds = Math.floor(time_left % 60);

    const minute_string = minutes < 10 ? '0' + minutes : minutes;
    const second_string = seconds < 10 ? '0' + seconds : seconds
    return `${minute_string}:${second_string}`;
});

let intervalId = setInterval(() => {
    elapsed_time.value += 1;
}, 1000);

onUnmounted(() => {
    if (intervalId) {
        clearInterval(intervalId);
    }
});

</script>


<template>
    <div class="timer">
        <div>
            {{ task_time }}
        </div>
        <div>
            {{ formattedTime }}
        </div>
    </div>
</template>

<style scoped>
.timer {
    font-size: 24px;
}
</style>
