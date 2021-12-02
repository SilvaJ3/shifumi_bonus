<template>
  <!-- Affichage score -->
    <div class="flex justify-between items-center w-2/5 rounded-md border border-white px-3 py-2">
      <div class="text-white flex flex-col justify-center">
        <span class="font-bold text-xl my-0 py-0 leading-none" v-for="(tool, index) in tools" :key="index">{{ tool}}</span>
      </div>
      <div class="rounded-md bg-white py-2 px-8 flex flex-col justify-center items-center">
        <span>SCORE</span>
        <h1 class="text-4xl font-bold">{{score}}</h1>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      tools: ["ROCK", "PAPER", "SCISSORS", "LIZARD", "SPOCK"]
    }
  },
  props: {
    score: Number
  }
}
</script>

<style>

</style>