<template>
  <div class="wrapper">
    <h1 v-html="question.question"></h1>
    <b-button
      variant="success"
      :class="{ selected: answer }"
      @click="answer = true"
      >True</b-button
    >
    <b-button
      variant="danger"
      :class="{ selected: !answer && answer !== null }"
      @click="answer = false"
      >False</b-button
    >
    <b-button
      :disabled="answer === null"
      variant="dark"
      @click="
        nextQuestion();
        evaluateAnswer();
      "
      >Submit</b-button
    >
  </div>
</template>
<script>
export default {
  props: {
    question: Object,
    nextQuestion: Function,
    countScore: Function
  },
  data() {
    return {
      questionText: "",
      answer: null
    };
  },
  watch: {
    question: {
      //   immediate: true,
      handler() {
        this.answer = null;
      }
    }
  },
  methods: {
    evaluateAnswer() {
      let isCorrect = false;
      let correctAnswer = JSON.parse(
        this.question.correct_answer.toLowerCase()
      );
      if (this.answer === correctAnswer) {
        isCorrect = true;
      }
      this.countScore(isCorrect);
    }
  }
};
</script>
<style scoped>
.btn-danger,
.btn-primary {
  margin-left: 2em;
}
.btn-dark {
  display: block;
  margin: auto;
  margin-top: 2em;
}
.selected {
  border: 5px solid black;
}
</style>
