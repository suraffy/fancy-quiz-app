<template>
  <div class="container">
    <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />

    <SubHeader
      :questionNumber="index + 1"
    ></SubHeader>
    
    <div class="row">
      <div class="col-md-8 offset-md-2">
        <QuestionBox
          v-if="questions.length"
          :currentQuestion="questions[index]"
          @next="next"
          @result="result"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header'
import SubHeader from './components/SubHeader'
import QuestionBox from './components/QuestionBox'

export default {
  name: 'App',
  components: {
    Header,
    SubHeader,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
    }
  },
  methods: {
    next() {
      if (this.index < this.questions.length - 1) {
        this.index++;
      }
    },
    result(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }

      this.numTotal++;
    }
  },
  created() {
    fetch('https://opentdb.com/api.php?amount=5&category=18&difficulty=easy&type=multiple')
      .then(response => response.json())
      .then(jsonData => this.questions = jsonData.results)
  }
}
</script>

<style scoped>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css')
</style>