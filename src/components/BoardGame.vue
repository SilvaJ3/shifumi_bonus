<template>
  <div class="flex flex-col justify-center items-center w-full">

    <!-- Tableau de jeu -->

    <div class="board flex flex-col justify-center mt-10 w-1/2 h-96" v-if="!inGame">
      <div class="flex justify-center">
        <Tool :data="tools[0]" v-bind:style="'border:' + tools[0].color" @selection="play"/>
      </div>
      <div class="flex justify-evenly">
        <Tool :data="tools[1]" class="mr-4" v-bind:style="'border:' + tools[1].color" @selection="play"/>
        <Tool :data="tools[2]" class="ml-4" v-bind:style="'border:' + tools[2].color" @selection="play"/>
      </div>
      <div class="flex justify-center mt-16">
        <Tool :data="tools[3]" class="mr-8 mt-3" v-bind:style="'border:' + tools[3].color" @selection="play"/>
        <Tool :data="tools[4]" class="ml-8 mt-3" v-bind:style="'border:' + tools[4].color" @selection="play"/>
      </div>
    </div>

    <!-- Resultats -->

    <div v-else class="flex w-full h-96 mt-10">
      <div class="flex flex-col justify-center" :class="timerOut === true ? 'w-1/3 items-end' : 'w-1/2 items-center'">
        <h1 class="text-white mb-10">YOU PICKED</h1>
        <Tool :data="choiceData" v-bind:style="'border:' + choiceData.color"/>
      </div>
      <div class="w-1/3 flex flex-col justify-center items-center" v-if="timerOut">
        <h1 class="text-white text-4xl mb-5">{{result}}</h1>
        <div class="rounded-md bg-white py-2 px-8 cursor-pointer" @click="reset()">
          <h1>PLAY AGAIN</h1>
        </div>
      </div>
      <div class="flex flex-col justify-center" :class="timerOut === true ? 'w-1/3 items-start' : 'w-1/2 items-center'">
        <h1 class="text-white mb-10">THE HOUSE PICKED</h1>
        <div v-if="house === ''">
          <div class="rounded-full px-5 py-4 empty w-28 h-28 shadow-inner">
            
          </div>
        </div>
        <div v-else>
          <Tool :data="houseData" v-bind:style="'border:' + houseData.color"/>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import Tool from "./Tool.vue"

// import des images
import paper from "../assets/images/icon-paper.svg"
import rock from "../assets/images/icon-rock.svg"
import scissors from "../assets/images/icon-scissors.svg"
import lizard from "../assets/images/icon-lizard.svg"
import spock from "../assets/images/icon-spock.svg"


export default {
  data(){
    return{
      tools: [
        {
          name: "scissors",
          image: scissors,
          color: "solid 10px hsl(39, 89%, 49%);",
        },
        {
          name: "spock",
          image: spock,
          color: "solid 10px hsl(189, 58%, 57%);",
        },
        {
          name: "paper",
          image: paper,
          color: "solid 10px hsl(230, 89%, 62%);",
        },
        {
          name: "rock",
          image: rock,
          color: "solid 10px hsl(349, 70%, 56%);",
        },
        {
          name: "lizard",
          image: lizard,
          color: "solid 10px hsl(261, 72%, 63%);",
        },
      ],
      inGame: false,
      choice: ["scissors", "spock", "paper", "rock", "lizard"],
      player: "",
      house: "",
      timerOut: false,
      result: "",
      choiceData: null,
      houseData: null,
      score: 0,
      streak: 0
    }
  },
  components: {
    Tool
  },
  methods: {
    reset() {
      this.timerOut = false;
      this.inGame = false;
      this.house = "";
      this.result = "";
      this.choiceData = null;
      this.houseData = null;
    },
    play(value) {
      this.inGame = true;
      this.choiceData = this.tools[this.choice.indexOf(value)];
      if (value == "paper") {
        this.player = value;
      } else if (value == "scissors"){
        this.player = value;
      } else if (value == "rock") {
        this.player = value;
      } else if (value == "spock") {
        this.player = value;
      } else {
        this.player = value;
      }
      let random = Math.floor((Math.random() * this.choice.length));


      setTimeout(() => {
        this.house = this.choice[random];
        this.houseData = this.tools[this.choice.indexOf(this.house)];
        if (this.player === this.house) {
          this.result = "It's a draw";
          this.timerOut = true;
        } 
        // PAPER
        else if (this.player === "paper") {
          if (this.house === "rock" || this.house === "spock") {
            this.result = "YOU WIN";
            if(this.streak >= 5) {
              this.score += 2;
            } else {
              this.score++;
            }
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.streak = 0;
            this.timerOut = true;
          }
        } 
        // SCISSORS
        else if (this.player === "scissors") {
          if (this.house === "paper" || this.house === "lizard") {
            this.result = "YOU WIN";
            if(this.streak >= 5) {
              this.score += 2;
            } else {
              this.score++;
            }
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.streak = 0;
            this.timerOut = true;
          }
        } 
        // ROCK
        else if (this.player === "rock") {
          if (this.house === "scissors" || this.house === "lizard") {
            this.result = "YOU WIN";
            if(this.streak >= 5) {
              this.score += 2;
            } else {
              this.score++;
            }
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.streak = 0;
            this.timerOut = true;
          }
        }
        // LIZARD
        else if (this.player === "lizard") {
          if (this.house === "spock" || this.house === "paper") {
            this.result = "YOU WIN";
            if(this.streak >= 5) {
              this.score += 2;
            } else {
              this.score++;
            }
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.streak = 0;
            this.timerOut = true;
          }
        }
        // SPOCK
        else if (this.player === "spock") {
          if (this.house === "scissors" || this.house === "rock") {
            this.result = "YOU WIN";
            if(this.streak >= 5) {
              this.score += 2;
            } else {
              this.score++;
            }
            this.timerOut = true;
          } else {
            this.result = "YOU LOSE";
            this.score--;
            this.streak = 0;
            this.timerOut = true;
          }
        }

        this.$emit("score", this.score)
      }, 2000);

    },
  }
}
</script>

<style>

.board {
  background-image: url("../assets/images/bg-pentagon.svg");
  background-repeat: no-repeat;
  background-position: center;
}

.empty {
  background-color:hsl(237, 49%, 15%);
}

</style>