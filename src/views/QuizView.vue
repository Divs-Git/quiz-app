<template>
  <div>
    <QuizHeader :questionStatus="questionStatus" />
    <div>
      <Question :question="quiz.questions[currQuesIdx]" />
    </div>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'
import Question from '../components/Question.vue'
import QuizHeader from '../components/QuizHeader.vue'
import { ref, watch } from 'vue'
import quizes from '../data/quiz.json'

const route = useRoute()
const quizID = parseInt(route.params.id)
const currQuesIdx = ref(0)

const quiz = quizes.find((q) => q.id === quizID)

const questionStatus = ref(`${currQuesIdx.value}/${quiz.questions.length}`)
watch(
  () => currQuesIdx.value,
  () => {
    questionStatus.value = `${currQuesIdx.value}/${quiz.questions.length}`
  }
)
</script>

<style scoped></style>
