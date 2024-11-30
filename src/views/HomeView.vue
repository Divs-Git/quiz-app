<template>
  <header>
    <h1>Quizes</h1>
    <input
      type="text"
      name=""
      id=""
      placeholder="Search..."
      v-model.trim="search"
    />
  </header>
  <div class="options-container">
    <TransitionGroup appear @before-enter="beforeEnter" @enter="enter">
      <Card
        v-for="(quiz, index) in quizes"
        :key="quiz.id"
        :quiz="quiz"
        :data-index="index"
      />
    </TransitionGroup>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import q from '../data/quiz.json'
import Card from '../components/Card.vue'
import gsap from 'gsap'

const quizes = ref(q)
const search = ref('')

watch(search, () => {
  quizes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  )
})

// Transition
const beforeEnter = (el) => {
  // card-enter-from
  el.style.opacity = 0
  el.style.transform = 'translateY(-100px)'
}

const enter = (el) => {
  // card-enter-to
  // el.style.opacity = 1
  // el.style.tranform = 'translateY(0)'
  gsap.to(el, {
    y: 0,
    opacity: 1,
    duration: 0.3,
    delay: el.dataset.index * 0.3,
  })
}
</script>

<style scoped>
header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}
</style>
