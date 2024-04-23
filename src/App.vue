<script setup lang="ts">
import { ref } from 'vue';
import TimerDisplay from './components/TimerDisplay.vue'

const test_task_time = ref<number>(5);
</script>

<template>
    <div>
        <TimerDisplay :task_time="test_task_time" />
    </div>
</template>

<style scoped></style>
