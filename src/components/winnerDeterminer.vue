<script setup lang="ts">
import { ref, watch } from 'vue';

const props = defineProps<{
    gamePlayed: boolean;
    player1: string;
    player2: string;
}>();

let winner = ref<0 | 1 | 2>(0);
const emit = defineEmits(['winnerDefined', 'winner.value']);

watch(
    () => props.gamePlayed,
    () => {
        if (props.gamePlayed && props.player1 && props.player2) {
            switch (props.player1 + props.player2) {
                case 'RockRock':
                case 'PaperPaper':
                case 'ScissorsScissors':
                    winner.value = 0;
                    break;
                case 'RockScissors':
                case 'ScissorsPaper':
                case 'PaperRock':
                    winner.value = 1;
                    break;
                case 'ScissorsRock':
                case 'PaperScissors':
                case 'RockPaper':
                    winner.value = 2;
                    break;
            }
            emit('winnerDefined', 'winner.value');
        }
    }
);
</script>

<template>
    <div></div>
</template>

<style scoped></style>
