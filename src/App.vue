<template>
  <div id="app">
    <Score
      v-if="index < 10"
      :correctAns="correctAns"
      :totalAns="totalAns"
    ></Score>
    <Body
      v-if="questions.length > 0 && index < 10"
      :question="questions[index]"
      :nextQuestion="nextQuestion"
      :countScore="countScore"
    ></Body>
    <div v-if="index >= 10">
      <p>Good Job!</p>
      <p>You got {{ correctAns }} out of {{ totalAns }} questions right</p>
      <b-button @click="reset">Retry</b-button>
    </div>
  </div>
</template>

<script>
import Body from "./components/Body.vue";
import Score from "./components/Score.vue";

export default {
  name: "App",
  components: {
    Body,
    Score
  },
  data() {
    return {
      questions: [],
      index: 0,
      correctAns: 0,
      totalAns: 0
    };
  },
  methods: {
    nextQuestion() {
      this.index++;
    },
    countScore(isCorrect) {
      if (isCorrect) this.correctAns++;
      this.totalAns++;
    },
    reset() {
      this.index = 0;
      this.totalAns = 0;
      this.correctAns = 0;
    }
  },
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&type=boolean")
      .then(response => response.json())
      .then(question_json => {
        this.questions = question_json.results;
      });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
