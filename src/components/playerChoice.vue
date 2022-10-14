<script setup lang="ts">
import { ref, watch } from 'vue';

type RPS = 'Rock' | 'Paper' | 'Scissors';

const props = defineProps<{
    running: boolean;
    choice: RPS | null;
}>();

</script>

<template>
    <div class="human-result">
        <img
            src="/src/assets/rock.svg"
            alt="ROCK"
            v-if="!running && choice == 'Rock'"
        />
        <img
            src="/src/assets/paper.svg"
            alt="PAPER"
            v-if="!running && choice == 'Paper'"
        />
        <img
            src="/src/assets/scissors.svg"
            alt="SCISSORS"
            v-if="!running && choice == 'Scissors'"
        />
        <img
            src="/src/assets/handleft.svg"
            alt="?"
            v-if="!running && !choice"
        />
    </div>
</template>

<style scoped>
button {
    all: unset;
}

.human-result img {
    height: 200px;
    margin: 20px;
    filter: drop-shadow(0px 0px 28px #ffffff);
}
</style>
