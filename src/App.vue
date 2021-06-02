<template>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Start</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <Results v-show="score" :score="score" />
</template>

<script>
import Block from './components/Block.vue';
import Results from './components/Results.vue';

export default {
  name: "App",
  components: {
    Block,
    Results
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null
    };
  },
  methods: {
    start() {
      this.score = null;
      this.isPlaying = true;
      this.delay = 2000 + Math.round(Math.random() * 5000);
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
    }
  }
};
</script>

<style lang="sass">
body
  margin: 0
</style>
