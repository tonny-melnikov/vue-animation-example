<template lang="html">
  <div class="container white">
    <br><br>
    <h1 class="header center teal-text text-lighten-2">Answer please:</h1>
    <div class="row center">
      <h5 class="header col s12 green-text">{{ question }}</h5>
    </div>
    <div class="row center">
      <a href="!#"
        class="btn-large waves-effect waves-light teal lighten-1"
        @click.prevent="onAnswer(btnData[0].correct)">{{ btnData[0].text }}</a>
      <a href="!#"
        class="btn-large waves-effect waves-light teal lighten-1"
        @click.prevent="onAnswer(btnData[1].correct)">{{ btnData[1].text }}</a>
      <a href="!#"
        class="btn-large waves-effect waves-light teal lighten-1"
        @click.prevent="onAnswer(btnData[2].correct)">{{ btnData[2].text }}</a>
      <a href="!#"
        class="btn-large waves-effect waves-light teal lighten-1"
        @click.prevent="onAnswer(btnData[3].correct)">{{ btnData[3].text }}</a>
    </div>
    <br><br>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      question: 'Some default question',
      btnData: [
        { text: 'default text', correct: true },
        { text: 'default text', correct: true },
        { text: 'default text', correct: true },
        { text: 'default text', correct: true },
      ],
    };
  },
  methods: {
    onAnswer: function(isCorrect) {
      this.$emit('onAnswer', isCorrect);
    },
    generateRandomNumber: function(min, max, except) {
      var rand = Math.floor(Math.random() * (max - min + 1)) + min;
      if (except && except.indexOf(rand) !== -1 ) return this.generateRandomNumber(min, max, except);
      return rand;
    },
    makeQuestion: function () {
      this.mode = this.generateRandomNumber(0, 1);
      var num1 = this.generateRandomNumber(0, 100);
      var num2 = this.generateRandomNumber(1, 100);
      var result = num1 + num2;
      this.question = 'What is the result of ' + num1 + ' + ' + num2 + ' ?';
      if (!this.mode) {
        result = num1 - num2;
        this.question = 'What is the result of ' + num1 + ' - ' + num2 + ' ?';
      }
      var exc = [result];
      for (var i = 0; i < 4; i += 1) {
        var num = this.generateRandomNumber(result - 10, result + 10, exc);
        this.btnData[i] = {
          text: num,
          correct: false,
        };
        exc.push(num);
      }
      var correctIndex = this.generateRandomNumber(0, 3);
      this.btnData[correctIndex] = {
        text: result,
        correct: true,
      };
    }
  },
  created() {
    this.makeQuestion();
  },
}
</script>

<style lang="css">
</style>
