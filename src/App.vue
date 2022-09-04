<template>
  <div :class="{transition : isPlaying}" :style="{ background }" class="container">
    <h1 :class="{transition : isPlaying}" :style="{ color }">Reaction Timer</h1>
    <a :closed="isPlaying" href="#" :class="{transition : isPlaying}" @click="start" :style="{background, color, 'border-color': color }">play</a>
    <Block v-if="isPlaying" :delay="delay" @end="endGame"></Block>
    <Results v-if="showResults" :score="score" />
  </div>
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
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
      score: null,
      showResults: false,
      background: "#fff",
      color: "#000",
    };
  },
  methods: {
    start(e) {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;
      this.background = "red";
      this.color = "#fff";
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResults = true;
      this.background = "green";
      this.color = "#fff";
    },
  },
};
</script>

<style>
 .transition{
  transition:  2s ease-in ;
  transition-property: background, color, border;
} 

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  height: 100vh;
}

.container {
  padding: 20px;
  height: 100%;
}

.container a {
  color: #000;
  display: inline-block;
  padding: 10px 40px;
  border: 1px solid;
  border-color: #000;
  margin-top: 10px;
  cursor: pointer;
}

.container a[closed="true"] {
  opacity: 0.4;
  cursor: not-allowed;
}
</style>
