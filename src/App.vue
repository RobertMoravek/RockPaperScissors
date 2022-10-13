<script setup lang="ts">
import { ref } from 'vue';
import cpuPlayer from './components/cpuPlayer.vue';
import playerInput from './components/playerInput.vue';
import scoreKeeper from './components/scoreKeeper.vue';
import runningAnimation from './components/runningAnimation.vue';

type RPS = 'Rock' | 'Paper' | 'Scissors';

interface Results {
    player1: null | RPS;
    player2: null | RPS;
}

let running = ref<boolean>(false);
let winner = ref<0 | 1 | 2>(0);
let results = ref<Results>({ player1: null, player2: null });

function toggleRunning(): void {
    winner.value = 0;
    results.value.player1 = null;
    running.value = !running.value;

}

function setPlayerChoice(choice: RPS): void {
    if (running.value) {
        results.value.player1 = choice;
    }
}

function setCpuChoice(choice: RPS): void {
    results.value.player2 = choice;
    running.value = false;
    determineWinner();
}

function determineWinner(): void {
    if (results.value.player1 && results.value.player2) {
        switch (results.value.player1 + results.value.player2) {
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
    } else {
        winner.value = 2;
    }
}
</script>

<template>
    <header></header>

    <main>
        <scoreKeeper :winner="winner" />
        <div class="playing-field">
            <runningAnimation v-if="running" />
            <div class="human-result">
                <img
                    src="/src/assets/rock.svg"
                    alt="ROCK"
                    v-if="!running && results.player1 == 'Rock'"
                />
                <img
                    src="/src/assets/paper.svg"
                    alt="PAPER"
                    v-if="!running && results.player1 == 'Paper'"
                />
                <img
                    src="/src/assets/scissors.svg"
                    alt="SCISSORS"
                    v-if="!running && results.player1 == 'Scissors'"
                />
                <img
                    src="/src/assets/handleft.svg"
                    alt="?"
                    v-if="!running && !results.player1"
                />
            </div>
            <cpuPlayer
                :running="running"
                @cpu-has-chosen="setCpuChoice($event)"
            />
        </div>
        <div class="controlls">
            <playerInput
                @player-has-chosen="setPlayerChoice($event)"
                v-if="running"
            />
            <button>
                <img
                    src="/src/assets/playkey.png"
                    class="key"
                    alt="Play"
                    @click="toggleRunning"
                    v-if="!running"
                />
            </button>
        </div>
    </main>
</template>

<style scoped>
main {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    /* justify-content: center; */
    align-items: center;
}
.playing-field {
    width: 80%;
    height: 70%;
    min-height: 70%;
    max-height: 70%;
    display: flex;
    justify-content: center;
    align-items: center;
}

button {
    all: unset;
}

.key {
    height: 75px;
}

.human-result img {
    height: 200px;
    margin: 20px;
    filter: drop-shadow(0px 0px 28px #FFFFFF);
}
.controlls button:focus img {
    transform: translate(1px, 3px);
    filter: drop-shadow(2px 2px 2px #474747);
}
.controlls img {
    filter: drop-shadow(3px 5px 3px #474747);
}
</style>
