<template>
  <div id="app">
    <oQuiz 
    titleColor="#fafafa" 
    quizTitle="Title Placeholder" />
  </div>
</template>

<script>
import oQuiz from './components/oQuiz.vue'

export default {
  name: 'App',
  components: {
    oQuiz
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
