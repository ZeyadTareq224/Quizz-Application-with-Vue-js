<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :numTotal="numTotal"/>
    <QuestionBox :increment="increment" :currentQuestion="questions[index]" :next="next" v-if="questions.length"/>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import QuestionBox from './components/QuestionBox.vue';

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return {  
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal:0
    }
  },
  methods:{
    next(){
      this.index = this.index + 1
      if (this.index >= 10){
        this.index = 0
      } 
    },
    increment(isCorrect){
      if (isCorrect){
        this.numCorrect++
      }
      this.numTotal++
      },
  },
  mounted: function(){
      fetch('https://opentdb.com/api.php?amount=30&type=multiple',
      {
        method: 'get'
      })
      .then((res) => {
        return res.json()
      })
      .then((data) => {
        this.questions = data.results
      })
  }
}
</script>

<style scoped>

</style>
