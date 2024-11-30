<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question
        v-if="!showResult"
        :question="quiz.questions[currQuesIdx]"
        @selectOption="optionSelected"
      />
      <Result
        v-else
        :quizQuestionLength="quiz.questions.length"
        :totalCorrectAnsCount="totalCorrectAnsCount"
      />
    </div>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'
import Question from '../components/Question.vue'
import QuizHeader from '../components/QuizHeader.vue'
import { computed, ref } from 'vue'
import quizes from '../data/quiz.json'
import Result from '../components/Result.vue'

const route = useRoute()
const quizID = parseInt(route.params.id)
const currQuesIdx = ref(0)
const totalCorrectAnsCount = ref(0)
const showResult = ref(false)

const quiz = quizes.find((q) => q.id === quizID)

const questionStatus = computed(
  () => `${currQuesIdx.value}/${quiz.questions.length}`
)

const barPercentage = computed(
  () => `${(currQuesIdx.value / quiz.questions.length) * 100}%`
)

const optionSelected = (isCorrect) => {
  if (isCorrect) {
    totalCorrectAnsCount.value++
  }

  if (quiz.questions.length - 1 === currQuesIdx.value) {
    showResult.value = true
  }
  currQuesIdx.value++
}
</script>

<style scoped></style>
