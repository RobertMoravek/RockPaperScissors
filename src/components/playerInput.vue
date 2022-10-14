<script setup lang="ts">
import { ref, watch } from 'vue';

type RPS = 'Rock' | 'Paper' | 'Scissors';
enum Result {
    Rock = 'Rock',
    Paper = 'Paper',
    Scissors = 'Scissors'
}
let choice = ref<RPS>();

const emit = defineEmits<{
    (e: 'player-has-chosen', result: RPS): void;
}>();

watch(choice, (value) => {
    choice.value && emit('player-has-chosen', choice.value);
});
</script>

<template>
    <div class="player-keys">
        <button>
            <img
                src="/src/assets/rockkey.png"
                class="key"
                alt="ROCK"
                @click="choice = Result.Rock"
            />
        </button>
        <button>
            <img
                src="/src/assets/paperkey.png"
                class="key"
                alt="PAPER"
                @click="choice = Result.Paper"
            />
        </button>
        <button>
            <img
                src="/src/assets/scissorskey.png"
                class="key"
                alt="SCISSORS"
                @click="choice = Result.Scissors"
            />
        </button>
    </div>
</template>

<style scoped>

button {
    all: unset;
    height: 100%;
}
.player-keys {
    display: flex;
    gap: 20px;
    justify-content: center;
    align-items: flex-end;
    height: 100%;
    max-width: 300px;
}


.player-keys button:focus img {
    transform: translate(1px, 3px);
    filter: drop-shadow(2px 2px 2px #474747);
}
button .key {
    cursor: pointer;
    filter: drop-shadow(3px 5px 3px #474747);
    max-height: 100%;
    max-width: 80px;
}

</style>
