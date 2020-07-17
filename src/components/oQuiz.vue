<template>
  <div v-if="currentCuestion" class="oQuiz">
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
          class="button"
          :disabled="isDisabled"
        >
        {{answer.text}}
        </button>
      </div>
    </div>
    <transition name="fade"> 
      <div class="modal modal-correct" v-if="result === 'Correct'">{{result}}</div>
      <div class="modal modal-incorrect" v-if="result === 'Incorrect'">{{result}}</div>
    </transition>
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
          },
      ],

      currentQuestion: 0,
      
      showResult: false,
      result: null,
      isDisabled: false,
      summary: []
    }               
  },
  methods: {
    answerQuestion(answer){
      switch(answer.isCorrect){
        case true:
          this.showResult = true 
          this.result = 'Correct'
          this.isDisabled = true
          setTimeout(() => {
            this.showResult = false 
            this.result = null
            this.isDisabled = false
            if(this.currentQuestion < (this.quiz.length - 1)){
              this.currentQuestion++
            } else this.currentQuestion = 0 // must move user to summary 
            this.summary.push(1)
          }, 1000)
          break;
        
        case false:
          this.showResult = true 
          this.result = 'Incorrect'
          this.isDisabled = true
          setTimeout(() => {
            this.showResult = false
            this.result = null
            this.isDisabled = false
            if(this.currentQuestion < (this.quiz.length - 1)){
              this.currentQuestion++
            } else this.currentQuestion = 0 // must move user to summary 
            this.summary.push(0)
          }, 1000)
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
  
.modal
  position absolute
  top 30%
  z-index 2
  border-radius 5px
  text-align center
  padding 30px
  transition: width 2s, height 2s, background-color 2s, transform 2s;

.modal-incorrect
    background-color #cf6679
    

.modal-correct
  background-color #03dac6

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
    
</style>
