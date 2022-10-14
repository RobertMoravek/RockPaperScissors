<script setup lang="ts"></script>

<template>
    <!-- Just an animation of two hands going up and down endlessly -->
    <div class="running-animation">
        <img src="/src/assets/handleft.svg" alt="Left Hand" />
        <img src="/src/assets/handright.svg" alt="Right Hand" />
    </div>
</template>

<style scoped>
.running-animation img {
    height: 200px;
    width: 130px;
    -webkit-animation: slide-top 0.3s cubic-bezier(0.165, 0.84, 0.44, 1)
        infinite alternate-reverse both;
    animation: slide-top 0.3s cubic-bezier(0.165, 0.84, 0.44, 1) infinite
        alternate-reverse both;
    margin: 10px;

}



@-webkit-keyframes slide-top {
    0% {
        -webkit-transform: translate(0, 15vh);
        transform: translate(0, 15vh);
    }
    100% {
        -webkit-transform: translate(0, -25vh);
        transform: translateY(0, -25vh);
    }
}
@keyframes slide-top {
    0% {
        -webkit-transform: translate(0, 15vh);
        transform: translate(0, 15vh);
    }
    100% {
        -webkit-transform: translate(0, -25vh);
        transform: translateY(0, -25vh);
    }
}
</style>
