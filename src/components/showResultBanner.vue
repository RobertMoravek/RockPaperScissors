<script setup lang="ts">
const props = defineProps<{
    winner: null | 0 | 1 | 2;
}>();
</script>

<template>
    <!-- If a winner (or draw) was set, then display the matching banner -->
    <div class="results-banner">
        <img src="/src/assets/win.png" alt="YOU WIN!" v-show="winner === 1" />
        <img src="/src/assets/lose.png" alt="YOU LOSE!" v-show="winner === 2" />
        <img src="/src/assets/draw.png" alt="DRAW!" v-show="winner === 0" />
    </div>
</template>

<style scoped>
.results-banner {
    position: absolute;
    top: 18%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 120%;
    display: flex;
    justify-content: center;
}

.results-banner img {
    width: 100%;
    max-width: 400px;
    filter: drop-shadow(0px 0px 28px #ffffff);
}
</style>
