<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps<{
    winner: 0 | 1 | 2;
}>();

interface Score {
    player1: number;
    player2: number;
}
let score = ref<Score>({
    player1: 0,
    player2: 0
});
const emit = defineEmits(['scoreKeepingDone']);

watch(
    () => props.winner,
    (winner) => {
        if (props.winner > 0) {
            if (winner === 1) {
                score.value.player1++;
                score.value.player2 > 0 && score.value.player2--;
            } else {
                score.value.player2++;
                score.value.player1 > 0 && score.value.player1--;
            }
            emit('scoreKeepingDone');
        }
    }
);
</script>

<template>
    <div>
        <p>{{ score.player1 }} : {{ score.player2 }}</p>
    </div>
</template>

<style scoped>

</style>
