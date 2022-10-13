<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps<{
    running: boolean;
}>();

enum Result {
    Rock = 'Rock',
    Paper = 'Paper',
    Scissors = 'Scissors'
}
let result = ref<string>('');
const emit = defineEmits(['cpuGameDone']);

watch(
    () => props.running,
    (value) => {
        let numResult: number = Math.floor(Math.random() * 3);
        switch (numResult) {
            case 0:
                result.value = Result.Rock;
                break;
            case 1:
                result.value = Result.Paper;
                break;
            case 2:
                result.value = Result.Scissors;
                break;
        }
        emit('cpuGameDone', 'result.value');
    }
);
</script>

<template>
    <div class="cpu-result">
        <img src="/src/assets/rock.svg" alt="ROCK" v-if="result == 'Rock'" />
        <img src="/src/assets/paper.svg" alt="PAPER" v-if="result == 'Paper'" />
        <img
            src="/src/assets/scissors.svg"
            alt="SCISSORS"
            v-if="result == 'Scissors'"
        />
    </div>
</template>

<style scoped>
.cpu-result {
}
.cpu-result img {
    height: 200px;
}
</style>
