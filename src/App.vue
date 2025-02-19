<template>
  <div id="app">
    <h1>Викторина: Твой путь в IT</h1>
    <QuizQuestion
      v-if="!showResult && currentQuestionIndex < questions.length"
      :question="questions[currentQuestionIndex]"
      @answer="handleAnswer"
    />
    <QuizResult v-else :result="resultText" />
  </div>
</template>

<script>
import { ref } from 'vue'
import QuizQuestion from './components/QuizQuestion.vue'
import QuizResult from './components/QuizResult.vue'

export default {
  components: { QuizQuestion, QuizResult },
  setup() {
    const questions = ref([
      {
        question: 'Как ты относишься к математике?',
        options: [
          { text: 'Обожаю решать задачи', value: '3' },
          { text: 'Нравится, но не всегда понимаю', value: '2' },
          { text: 'Не люблю, слишком сложно', value: '1' },
        ],
      },
      {
        question: 'Что тебе больше нравится?',
        options: [
          { text: 'Создавать сайты и интерфейсы', value: '1' },
          { text: 'Анализировать данные', value: '3' },
          { text: 'Разрабатывать игры', value: '2' },
        ],
      },
      {
        question: 'Какой способ обучения тебе удобнее?',
        options: [
          { text: 'Курсы и видеоуроки', value: '1' },
          { text: 'Практика и эксперименты', value: '2' },
          { text: 'Чтение книг и документации', value: '3' },
        ],
      },
      {
        question: 'Как ты относишься к креативным задачам?',
        options: [
          { text: 'Обожаю творческие задачи', value: '1' },
          { text: 'Нравится и логика, и креативность', value: '2' },
          { text: 'Больше предпочитаю строгую логику', value: '3' },
        ],
      },
      {
        question: 'Какой формат работы ты предпочитаешь?',
        options: [
          { text: 'Самостоятельная работа (фриланс)', value: '1' },
          { text: 'Работа в компании', value: '23' },
        ],
      },
      {
        question: 'Какая сфера тебя больше привлекает?',
        options: [
          { text: 'Разработка веб-сайтов', value: '1' },
          { text: 'Разработка серверной логики', value: '2' },
          { text: 'Анализ данных', value: '3' },
        ],
      },
      {
        question: 'Какую работу ты бы выбрал?',
        options: [
          { text: 'Создание красивых и удобных сайтов', value: '1' },
          { text: 'Анализ больших данных', value: '3' },
          { text: 'Оптимизация серверов и автоматизация', value: '2' },
        ],
      },
    ])

    const currentQuestionIndex = ref(0)
    const answers = ref([])
    const showResult = ref(false)
    const resultText = ref('')

    const handleAnswer = (answer) => {
      answers.value.push(answer)
      if (currentQuestionIndex.value === questions.value.length - 1) {
        calculateResult()
        showResult.value = true
      } else {
        currentQuestionIndex.value++
      }
    }

    const calculateResult = () => {
      const counts = { 1: 0, 2: 0, 3: 0 }
      answers.value.forEach((answer) => {
        ;[...answer].forEach((char) => {
          if (counts[char] !== undefined) counts[char]++
        })
      })

      const maxCategory = Object.keys(counts).reduce((a, b) => (counts[a] > counts[b] ? a : b))
      resultText.value =
        maxCategory === '1'
          ? 'Вам подходит Frontend!'
          : maxCategory === '2'
            ? 'Вам подходит Backend!'
            : 'Вам подходит Анализ данных!'
    }

    return { questions, currentQuestionIndex, showResult, resultText, handleAnswer }
  },
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 0;
  padding: 15px;
  box-sizing: border-box;
}

#app {
  max-width: 100%;
  overflow-x: hidden;
}

h1 {
  font-size: clamp(1.5rem, 5vw, 2.5rem);
  margin: 15px 0;
  padding: 0 10px;
}

@media (max-width: 480px) {
  body {
    padding: 10px;
  }
}
</style>
