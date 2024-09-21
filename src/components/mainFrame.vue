<template>
  <div v-show="isShow2">
    <h1 id="mainTitle">⛱&#xFE0E; Trivia Quiz</h1>
    <label for="search">🔍&#xFE0E; Search:</label>
    <input type="text" id="search" name="search" /><br /><br />
    <button v-on:click="searchQuestion()" class="btn-orange">
      🔍&#xFE0E; Search Question</button
    ><br /><br />
    <div
      style="
        width: 100%;
        height: 500px;
        overflow-y: auto;
        border: 1px solid black;
      "
    >
      <table style="width: 100%" id="t1">
        <tr>
          <th>Question</th>
          <th>Answer A</th>
          <th>Answer B</th>
          <th>Answer C</th>
          <th>Correct Answer</th>
        </tr>
        <tr v-for="i in alist" :key="i.QuestionNumber">
          <td>{{ i.Question }}</td>
          <td>{{ i.AnswerA }}</td>
          <td>{{ i.AnswerB }}</td>
          <td>{{ i.AnswerC }}</td>
          <td>{{ i.CorrectAnswer }}</td>
        </tr>
      </table>
    </div>
    <button id="gameBtn" class="btn-orange" v-on:click="openGF()">
      Start Game
    </button>
  </div>
</template>

<script>
import questions from './questions.json';
export default {
  name: "mainFrame",
  data() {
    return {
      alist: questions,
      blist: [],
      isShow2: true,
    };
  },
  mounted() {
    this.$root.$on("closeGF", () => {
      this.isShow2 = true;
    });
  },
  methods: {
    searchQuestion() {
      var input, filter, table, tr, td, i, txtValue;
      input = document.getElementById("search");
      filter = input.value;
      table = document.getElementById("t1");
      tr = table.getElementsByTagName("tr");
      for (i = 0; i < tr.length; i++) {
        td = tr[i].getElementsByTagName("td")[0];
        if (td) {
          txtValue = td.textContent || td.innerText;
          if (txtValue.indexOf(filter) > -1) {
            tr[i].style.display = "";
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    },
    openGF() {
      this.$root.$emit("openGF");
      this.isShow2 = false;
    },
  },
};
</script>
<style>
body {
  background: black;
  background-image: linear-gradient(to right, #434343 0%, black 100%);
  scroll-behavior: smooth;
}
h1,
h2,
h3,
h4,
h5,
h6,
label,
table {
  color: white;
}
table {
  border: 1px solid orange;
}
#gameBtn {
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
#mainTitle {
  animation: flow 2s ease-in-out infinite;
  background: linear-gradient(to right, #c6ffdd, #fbd786, #f7797d);
  background-size: 200%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
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
input {
  color: white;
  border-width: 1px;
  border-radius: 7px;
  background: #e96443;
  background: -webkit-linear-gradient(to right, #904e95, #e96443);
  background: linear-gradient(to right, #904e95, #e96443);
}
.currentQ {
  position: fixed;
  top: 5px;
  left: 5px;
  text-align: center;
  background: black;
  background-image: linear-gradient(to left, #434343 0%, black 100%);
  border: 1px solid orange;
  padding: 10px;
  border-radius: 10px;
  max-width: 30%;
}
</style>