<template>
  <div class="oQuiz">
    <div
      class="quiz-container"
    >
      <h1
        :style="{color: titleColor}"
        class="quiz-title"
      >
        {{quizTitle}}
      </h1>
      <div class="quiz-img-container">
        <img class="quiz-img" :src="quiz[currentQuestion].img">
      </div>
      <div class="question-container">
        <h2 class="question-title">{{quiz[currentQuestion].question }}</h2>
        <button
          @click="answerQuestion(answer)" 
          v-for="answer in quiz[currentQuestion].answers" 
          :key="answer.text" 
          class="answer"
        >
        {{answer.text}}
        </button>
      </div>
    </div>
    <h3 v-if="showResult">{{result}}</h3>
  </div>
</template>

<script>

export default {
  name: 'oQuiz',
  props: {
    msg: String,
    titleColor: String,
    quizTitle: String,
  },

  data() {
    return {
      quiz: [
          {img: 'https://img.tsargrad.tv/cache/b/8/-peterburg.jpg/w720h405fill.jpg', question: 'Who built Saint Petersburg?', answers: [
            {text: 'Napoleo', isCorrect: true},
            {text: 'Peter The Great', isCorrect: false}
            ]
          },
          {img: 'logo.png', question: 'Who killed John Kennedy', answers: [
            {text: 'Gorbachev', isCorrect: true},
            {text: 'Lenin', isCorrect: false}
            ]
          }
      ],

      currentQuestion: 0,
      
      showResult: false,
      result: null
    }               
  },
  methods: {
    nextQuestion() {
      if(this.currentQuestion < (this.quiz.length - 1)){
        this.currentQuestion++ // change behavior (check if answer === true then proceed to the nex question)
      } else this.currentQuestion = 0 // Change behaivor (summary of quiz)
    },

    answerQuestion(answer){
      switch(answer.isCorrect){
        case true:
          this.showResult = true 
          this.result = 'Correct'
          setTimeout(() => {
            this.showResult = false 
            this.result = null
          }, 2000)
          break;
        
        case false:
          this.showResult = true 
          this.result = 'Incorrect'
          setTimeout(() => {
            this.showResult = false
            this.result = null
          }, 2000)
          break;
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  .oQuiz
    display flex
    justify-content center

    .quiz-container
      border 2px solid #cf6679
      border-radius 3px
      padding 10px
      background-color #292929

      .quiz-title
        margin 0
        padding 0
        font-size 3rem
        color #cf6679

      .quiz-img-container
        display flex
        justify-content center
        
        .quiz-img
          width 100%
      
      .question-container
        .question-title
          color #ffffff
    
</style>
