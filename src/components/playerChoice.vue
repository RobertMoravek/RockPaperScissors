<script setup lang="ts">
import { ref, watch } from 'vue';

type RPS = 'Rock' | 'Paper' | 'Scissors';

const props = defineProps<{
    running: boolean;
    choice: RPS | null;
}>();

</script>

<template>
    <!-- If the game isn't running, then display the user's choice (or lack thereof) -->
    <div class="human-result">
        <img
            src="/src/assets/rock.svg"
            alt="ROCK"
            v-show="!running && choice == 'Rock'"
        />
        <img
            src="/src/assets/paper.svg"
            alt="PAPER"
            v-show="!running && choice == 'Paper'"
        />
        <img
            src="/src/assets/scissors.svg"
            alt="SCISSORS"
            v-show="!running && choice == 'Scissors'"
        />
        <img
            src="/src/assets/handleft.svg"
            alt="?"
            v-show="!running && !choice"
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
