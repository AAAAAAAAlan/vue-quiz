<template>
  <div class="oQuiz">
    <div v-if="finished" class="quiz-finish">
      <h1>{{`Congrats! Your results are: `}}</h1>
      <h2 class="result">{{`${this.summary.reduce((a,b) => a + b)} out of ${this.summary.length}`}}</h2>
    </div>
    <div
      class="quiz-container"
      v-if="finished === false"
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
        <div class="btn-container">
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
    quiz: Object
  },

  data() {
    return {
      currentQuestion: 0,
      showResult: false,
      result: null,
      isDisabled: false,
      summary: [],
      finished: false
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
            } else this.finished = true
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
            } else this.finished = true
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
    
    .quiz-finish
      padding 10px
      background-color #292929
      border 1px solid #EEF3F6
      box-sizing border-box
      border-radius 4px
      background #FFFFFF
      width: 400px;
      font-size 9pt

      .result
        text-align right

    .quiz-container
      padding 10px
      background-color #292929
      border 1px solid #EEF3F6
      box-sizing border-box
      border-radius 4px
      background #FFFFFF


      .quiz-title
        margin 0
        padding 0
        font-size 3rem
        color #cf6679
        
      .quiz-img-container
        display flex
        justify-content center
        
        .quiz-img
          width: 400px;
          height: auto;
          border-radius 4px
          
      
      .question-container
        .question-title
          color #19193E
          text-align center

        .btn-container
          display flex
          justify-content center

          button
            border none
            border-radius 3px
            padding 10px
            margin 0 10% 20px 10%
            background-color #ffffff
            font-size 12pt
            font-weight bold
            user-select none
            outline none
            border: 1px solid #4D1ED3;
            box-sizing: border-box;
            border-radius: 4px;

            &:hover
              background #4D1ED3 
              color white

            &:active
              bbackground #4D1ED3
  
.modal
  position absolute
  top 30%
  z-index 2
  border-radius 5px
  text-align center
  padding 30px
  transition: width 2s, height 2s, background-color 2s, transform 2s;

.modal-incorrect
    background-color #FC1946
    

.modal-correct
  background-color #72EBBA

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
    
</style>
