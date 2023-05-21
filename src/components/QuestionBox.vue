<template>
  <div class="jumbotron text-center">
    <h4>{{currentQuestion.question}}</h4>
    <hr class="my-4">

     <ul class="list-group mb-3">
      <li 
        class="list-group-item"
        :class="activeClass(index)"
        v-for="(answer, index) in answers"
        :key="index"
        @click="selectAnswer(index)"
      >
        {{answer}}
      </li>
    </ul>
    
    <button 
      class="btn btn-primary mx-2"
      :disabled="selectedIndex === null || submitted"
      @click="submitAnswer"
    >
      Submit
    </button>

    <button 
      class="btn btn-success mx-2"
      :disabled="!submitted"
      @click="$emit('next')"
    >
      Next
    </button>
  </div>
</template>

<script>
export default {
  name: 'QuestionBox',
  props: {
    currentQuestion: Object
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      answers: [],
      submitted: false,
      prevSelected: null,
    }
  },
  methods: {
    ShuffleAnswers() {
      const answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      const rand = Math.floor(Math.random() * answers.length)

      const temp = answers[rand]
      answers[rand] = this.currentQuestion.correct_answer
      answers[answers.length - 1] = temp

      this.correctIndex = rand

      this.answers = answers
    },
    selectAnswer(index) {
      this.selectedIndex = index
    },
    submitAnswer() {
      let isCorrect = false

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }

      this.$emit('result', isCorrect)

      this.submitted = true
      this.prevSelected = this.selectedIndex
    },
    activeClass(index) {
      return (
        !this.submitted && index === this.selectedIndex ? 'selected' : 
        this.submitted && index === this.correctIndex ? 'correct' :
        this.submitted && index === this.prevSelected ? 'incorrect' : ''
      )
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.ShuffleAnswers()
        this.submitted = false
      }
    }
  }
}
</script>

<style scoped>
.list-group-item {
  cursor: pointer;
}

.list-group-item:hover:not(.selected, .correct, .incorrect) {
  background-color: #f8f8f8;
}

.selected {
  background-color: rgb(212, 238, 255);
}

.correct {
  background-color: rgb(159, 255, 159);
}

.incorrect {
  background-color: rgb(255, 180, 167);
}
</style>