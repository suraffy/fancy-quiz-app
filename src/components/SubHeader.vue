<template>
  <div class="text-center">
    <h4>Question #{{questionNumber}}</h4>
    <p class="text-secondary">Tech related, 5 quesions</p>
  </div>
</template>

<script>
export default {
  name: 'SubHeader',
  props: {
    questionNumber: Number
  }
}
</script>

<style scoped>
</style>