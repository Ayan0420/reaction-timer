<template>
    <div class="container">
        <h1>Simple Reaction Timer</h1>
        <button @click="start" :disabled="isPlaying">play</button>
        <Block v-if="isPlaying" :delay="delay" @end="endGame" />
        <Results v-if="showResult" :score="score" />
    </div>
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

export default {
    name: "App",
    components: { Block, Results },
    data() {
        return {
            isPlaying: false,
            delay: null,
            score: null,
            showResult: false,
        };
    },
    methods: {
        start() {
            this.delay = 2000 + Math.random() * 5000;
            this.isPlaying = true;
            this.showResult = false;
        },
        endGame(reactionTime) {
            this.score = reactionTime;
            this.isPlaying = false;
            this.showResult = true;
        },
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.container {
    width: 40%;
    min-height: 70vh;
    border: #0f7caf solid;
    border-radius: 30px;
}

button {
    background: #0f7caf;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
}
button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
}
</style>
