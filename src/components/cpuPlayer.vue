<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps<{
    running: boolean;
}>();

type RPS = 'Rock' | 'Paper' | 'Scissors';

enum Result {
    Rock = 'Rock',
    Paper = 'Paper',
    Scissors = 'Scissors'
}
let result = ref<RPS>();
let showResult = ref<boolean>(false);

const emit = defineEmits<{
    (e: 'cpu-has-chosen', result: RPS): void;
}>();

// If running is changing and true...
watch(
    () => props.running,
    (value) => {
        if (props.running) {
            showResult.value = false;
            // ... wait 2 seconds, chose rock, paper or scissors...
            setTimeout(() => {
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
                // ... emit the result and set the variable to show it to true
                showResult.value = true;
                result.value && emit('cpu-has-chosen', result.value);
            }, 2000);
        }
    }
);
</script>

<template>
    <!-- If show result is true and there is a result, then show it -->
    <div class="cpu-result">
        <img
            src="/src/assets/rock.svg"
            alt="ROCK"
            v-if="showResult && result == 'Rock'"
        />
        <img
            src="/src/assets/paper.svg"
            alt="PAPER"
            v-if="showResult && result == 'Paper'"
        />
        <img
            src="/src/assets/scissors.svg"
            alt="SCISSORS"
            v-if="showResult && result == 'Scissors'"
        />
    </div>
</template>

<style scoped>
.cpu-result img {
    height: 200px;
    margin: 20px;
    filter: drop-shadow(0px 0px 28px #FFFFFF);
}
</style>
