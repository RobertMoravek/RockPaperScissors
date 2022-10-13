<script setup lang="ts">
import { ref } from 'vue';
import cpuPlayer from './components/cpuPlayer.vue';

let running = ref<boolean>(false);
let winner = ref<number>(0);

function toggleRunning(): void {
    running.value = !running.value;
    // console.log(running);
}

function printResult(e: string): void {
    running.value = false;
}
</script>

<template>
    <header></header>

    <main>
        <div class="playing-field">
            <cpuPlayer
                :running="running"
                :key="1"
                @cpu-game-done="printResult($event)"
            />
        </div>
        <button @click="toggleRunning">Play</button>
        <ScoreKeeper :winner="0" />
    </main>
</template>

<style scoped>
main {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.playing-field {
    width: 80%;
    height: 80%;
}
</style>
