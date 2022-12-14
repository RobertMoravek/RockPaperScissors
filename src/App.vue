<script setup lang="ts">
import { ref } from 'vue';
import cpuPlayer from './components/cpuPlayer.vue';
import playerInput from './components/playerInput.vue';
import scoreKeeper from './components/scoreKeeper.vue';
import runningAnimation from './components/runningAnimation.vue';
import playerChoice from './components/playerChoice.vue';
import showResultBanner from './components/showResultBanner.vue';

type RPS = 'Rock' | 'Paper' | 'Scissors';

interface Results {
    player1: null | RPS;
    player2: null | RPS;
}


let running = ref<boolean>(false); // Running variable controlls many Components
let results = ref<Results>({ player1: null, player2: null }); // What the player and the computer have chosen
let winner = ref<null | 0 | 1 | 2>(null);

// Starts a new round by resetting values and setting running to true
function toggleRunning(): void {
    winner.value = null;
    results.value.player1 = null;
    running.value = !running.value;
}

// Sets player choice, after receiving it from the Comp
function setPlayerChoice(choice: RPS): void {
    if (running.value) {
        results.value.player1 = choice;
    }
}

// Sets CPU choice, after receiving it from the Comp & ends the turn (time for player to decide)
function setCpuChoice(choice: RPS): void {
    results.value.player2 = choice;
    running.value = false;
    determineWinner();
}

// Determines, who won
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
        // If the player didn't chose, they lose
        winner.value = 2;
    }
}
</script>

<template>
    <main>
        <div class="score-keeper">
            <scoreKeeper :winner="winner" />
        </div>
        <div class="playing-field">
            <!-- Hands doing the rock, paper, scissors motion -->
            <runningAnimation v-if="running" /> 
            <!-- Displays, what the player chose -->
            <playerChoice :running="running" :choice="results.player1" />
            <!-- Choses and displays the cpu's choice  -->   
            <cpuPlayer  
                :running="running"
                @cpu-has-chosen="setCpuChoice($event)"
            />
            <!-- Shows who won -->
            <Transition>
                <showResultBanner :winner="winner" v-if="winner != null" />
            </Transition>
        </div>

        <div class="controlls">
            <!-- Shows the rock, paper and scissor button -->
            <playerInput
                @player-has-chosen="setPlayerChoice($event)"
                v-if="running"
            />
            <!-- Play button -->
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
    align-items: center;
}

.score-keeper {
    height: 15%;
}
.playing-field {
    width: 80%;
    height: 67%;
    min-height: 67%;
    max-height: 70%;
    display: flex;
    justify-content: center;
    align-items: center;
}

button {
    all: unset;
}

.human-result img {
    height: 200px;
    margin: 20px;
    filter: drop-shadow(0px 0px 28px #ffffff);
}

.controlls {
    width: 100%;
    height: 15%;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    margin-bottom: 1rem;
}

.controlls button {
    height: 100%;
}
.controlls button:focus img {
    transform: translate(1px, 3px);
    filter: drop-shadow(2px 2px 2px #474747);
}
button img {
    filter: drop-shadow(3px 5px 3px #474747);
    max-height: 100%;
    max-width: 300px;
}

.v-enter-active,
.v-leave-active {
    transition: opacity 0.2s ease-in;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>
