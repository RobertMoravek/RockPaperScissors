<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps<{
    winner: null | 0 | 1 | 2;
}>();

interface Score {
    player1: number;
    player2: number;
}
let score = ref<Score>({
    player1: 0,
    player2: 0
});


// If a winner was passed in and it's not null (rest state) or 0 (draw)....
watch(
    () => props.winner,
    (winner) => {
        if (props.winner && props.winner > 0) {
            // ... award the point to the correct player
            if (winner === 1) {
                score.value.player1++;
            } else {
                score.value.player2++;
            }
        }
    }
);
</script>

<template>
    <!-- Display the scores -->
    <div class="scores">
        <img src="/src/assets/playericon.png" alt="YOU" />
        <p>{{ score.player1 }} : {{ score.player2 }}</p>
        <img src="/src/assets/cpuicon.png" alt="CPU" />
    </div>
</template>

<style scoped>
.scores {
    display: flex;
    flex-direction: row;
    gap: 15px;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    margin-top: 1rem;
}

p {
    font-size: 3rem;
    color: white;
    font-family: Furore, sans-serif;
    text-shadow: 3px 5px 5px #474747;
    line-height: 3rem;
    width: 12rem;
    text-align: center;
}

img {
    height: 2.5rem;
}
</style>
