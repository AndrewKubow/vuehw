<template>
  <div id="app">
    <Header
    :nmbCorrect="nmbCorrect"
    :nmbTotal="nmbTotal"
    />
    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>

  </div>
</template>

<script>
import Header from './components/header.vue'
import QuestionBox from './components/questionBox.vue'

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return{
      questions: [],
      index: 0,
      nmbCorrect: 0,
      nmbTotal: 0
    }
  },
  methods: {
    next (){
      this.index++
    },
    increment(isCorrect){
      if (isCorrect){
        this.nmbCorrect++
      }
      this.nmbTotal++
    }

  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=25', {
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) =>{
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
