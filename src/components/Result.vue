<template>
  <div class="result">
    <p>Your Result...</p>
    <h1>{{ totalCorrectAnsCount }}/{{ quizQuestionLength }}</h1>
    <RouterLink to="/">Go Back To Home</RouterLink>
  </div>
</template>
<script setup>
import { RouterLink } from 'vue-router'

const props = defineProps(['quizQuestionLength', 'totalCorrectAnsCount'])
</script>
<style scoped>
.result {
  text-align: center;
  padding: 100px 0;
}

p {
  font-size: 25px;
}

h1 {
  font-size: 80px;
}
</style>
