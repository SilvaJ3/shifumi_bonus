<template>
  <div id="app" class="relative" :class="[showModal === true ? 'bg-gray-700' : '']">
    <section>
      <div class="container flex flex-col justify-center items-center">
        <ScoreBoard :score="score"/>
        <BoardGame @score="updateScore"/>
        <Rules />
      </div>
    </section>
  </div>
</template>

<script>
import ScoreBoard from "./components/ScoreBoard.vue"
import BoardGame from "./components/BoardGame.vue"
import Rules from "./components/Rules.vue"


export default {
  name: 'App',
  data() {
    return {
      score: 0,
    }
  },
  components: {
    ScoreBoard,
    BoardGame,
    Rules
  },
  methods: {
    updateScore(value){
      this.score = value;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Barlow Semi Condensed', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 5% 5% 1% 5%;
}

body {
  background: linear-gradient(to bottom, rgb(31, 55,86), rgb(20, 21, 57));
  background-repeat: no-repeat;
  margin: 0;
  box-sizing: border-box;
  height: 100vh;
}
</style>
