<template>
  <ul class="nav nav-tabs mb-3">
    <li class="nav-item">
      <span class="nav-link"><b>Fancy Quiz App</b></span>
    </li>
    <li class="nav-item">
      <span class="nav-link">Counter: {{ numCorrect }}/{{ numTotal }}</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'AppHeader',
  props: {
    numCorrect: Number,
    numTotal: Number
  }
}
</script>

<style scoped>
.nav-link {
  font-size: 1.4rem;
}
</style>