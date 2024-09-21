<template>
  <div v-show="isShow">
    <h1 id="mainTitle2">🎮&#xFE0E; The Game</h1>
    <h1>{{ this.alist[this.ansguess].Question }}</h1>
    <button v-on:click="guess('A')" class="btn-orange" id="A">
      {{ this.alist[this.ansguess].AnswerA }}</button
    ><br /><br />
    <button v-on:click="guess('B')" class="btn-orange" id="B">
      {{ this.alist[this.ansguess].AnswerB }}</button
    ><br /><br />
    <button v-on:click="guess('C')" class="btn-orange" id="C">
      {{ this.alist[this.ansguess].AnswerC }}</button
    ><br /><br />
    <h1 id="ic" style="color: lightgreen">Player Score: 2</h1>
    <h1 id="lc" style="color: lightcoral">Hunter Score: 0</h1>
    <button id="gameBtn2" class="btn-orange" v-on:click="closeGF()">
      Main Menu
    </button>
  </div>
</template>
<style>
.btn-orange {
  color: white;
  background: linear-gradient(
    180deg,
    #fff0e2,
    #fd7c05 8%,
    #744b2c 94%,
    #a94617
  );
  border-color: #fd7c05;
  border-radius: 10px;
  background-color: orange;
  font-size: 20px;
  margin-bottom: 5px;
  transition: 0.5s;
}
.btn-orange:hover,
.btn-orange:active,
.btn-orange:focus,
.btn-orange:visited {
  background: linear-gradient(
    180deg,
    #fff0e2,
    #5c2f06 8%,
    #994e0b 94%,
    #a94617
  );
  border-color: #422300;
  opacity: 0.7;
  cursor: pointer;
}
#gameBtn2 {
  position: fixed;
  top: 5px;
  right: 5px;
  width: 200px;
  height: 100px;
}
@keyframes flow {
  0% {
    background-position: 0 50%;
  }

  50% {
    background-position: 100% 50%;
  }

  100% {
    background-position: 0 50%;
  }
}
#mainTitle2 {
  animation: flow 2s ease-in-out infinite;
  background: linear-gradient(to right, #c6ffdd, #fbd786, #f7797d);
  background-size: 200%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
<script>
import questions from './questions.json';
var hunter = 0;
var player = 2;
export default {
  data() {
    return {
      isShow: false,
      alist: questions,
      ansguess: Math.floor((Math.random() * 100)*2.52),
    };
  },
  created() {
    this.$root.$on("openGF", () => {
      this.isShow = true;
    });
  },
  mounted() {
  },
  methods: {
    closeGF() {
      this.$root.$emit("closeGF");
      this.isShow = false;
      player = 2;
      hunter = 0;
      document.getElementById("ic").innerHTML = "Player Score: " + player;
      document.getElementById("lc").innerHTML = "Hunter Score: " + hunter;
      this.counter = 0;
    },
    guess(ans) {
      var lguess = Math.random();
      console.log(ans)
      console.log(this.alist[this.ansguess].CorrectAnswer)
      if (ans == this.alist[this.ansguess].CorrectAnswer) {
        player++;
        document.getElementById("ic").innerHTML = "Player Score: " + player;
        if (player >= 10) {
          alert("You won!");
          player = 2;
          hunter = 0;
          document.getElementById("ic").innerHTML = "Player Score: " + player;
          document.getElementById("lc").innerHTML = "Hunter Score: " + hunter;
          this.counter = 0;
        } else if (lguess < 0.75 && player < 10) {
          hunter++;
          document.getElementById("lc").innerHTML = "Hunter Score: " + hunter;
        }
      } else {
        if (lguess < 0.75 && player != hunter) {
          hunter++;
          if (player == hunter) {
            alert("You lost!");
            player = 2;
            hunter = 0;
            document.getElementById("ic").innerHTML = "Player Score: " + player;
            document.getElementById("lc").innerHTML = "Hunter Score: " + hunter;
            this.counter = 0;
          }
          document.getElementById("lc").innerHTML = "Hunter Score: " + hunter;
        }
      }
      document.getElementById(ans).blur();
      this.ansguess = Math.floor((Math.random() * 100)*0.73);
    },
  },
};
</script>