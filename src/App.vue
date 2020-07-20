<template>
  <div id="app">
    <oQuiz 
    titleColor="#19193E" 
    quizTitle="History Quiz"
    :quiz="quiz"
    />
  </div>
</template>

<script>
import oQuiz from './components/oQuiz.vue'

export default {
  name: 'App',
  components: {
    oQuiz
  },
  data() {
    return {
     quiz: [
          {img: 'https://img.tsargrad.tv/cache/b/8/-peterburg.jpg/w720h405fill.jpg', question: 'Who built Saint Petersburg?', answers: [
            {text: 'Napoleo', isCorrect: true},
            {text: 'Peter The Great', isCorrect: false}
            ]
          },
          {img: 'https://cdn.britannica.com/s:800x450,c:crop/32/172732-138-941D1E2C/overview-John-F-Kennedy.jpg', question: 'Who killed John Kennedy', answers: [
            {text: 'Gorbachev', isCorrect: true},
            {text: 'Lenin', isCorrect: false}
            ]
          },
      ],
    }
  },
}
</script>

<style>
body{
    background: #121212;
}
#app {
  margin-top: 50px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
