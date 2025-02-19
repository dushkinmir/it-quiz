<template>
  <div id="app">
    <header class="site-header">
      <div class="header-content">
        <div class="logo">
          <img src="/images/logo.png" width="50" />
        </div>
      </div>
    </header>
    <h1>Викторина: Твой путь в IT</h1>
    <QuizQuestion
      v-if="!showResult && currentQuestionIndex < questions.length"
      :question="questions[currentQuestionIndex]"
      @answer="handleAnswer"
    />
    <QuizResult v-else :result="resultText" @restart="restartQuiz" />
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
        question: 'Как ты относишься к математике? 🔢',
        options: [
          { text: '🎯 Обожаю решать задачи', value: '3' },
          { text: '🤔 Нравится, но не всегда понимаю', value: '2' },
          { text: '😅 Не люблю, слишком сложно', value: '1' },
        ],
      },
      {
        question: 'Что тебе больше нравится? 💭',
        options: [
          { text: '🎨 Создавать сайты и интерфейсы', value: '1' },
          { text: '📊 Анализировать данные', value: '3' },
          { text: '🎮 Разрабатывать игры', value: '2' },
        ],
      },
      {
        question: 'Какой способ обучения тебе удобнее? 📚',
        options: [
          { text: '🎥 Курсы и видеоуроки', value: '1' },
          { text: '⚡ Практика и эксперименты', value: '2' },
          { text: '📖 Чтение книг и документации', value: '3' },
        ],
      },
      {
        question: 'Как ты относишься к креативным задачам? 🎯',
        options: [
          { text: '🎨 Обожаю творческие задачи', value: '1' },
          { text: '⚖️ Нравится и логика, и креативность', value: '2' },
          { text: '🧮 Больше предпочитаю строгую логику', value: '3' },
        ],
      },
      {
        question: 'Какой формат работы ты предпочитаешь? 💼',
        options: [
          { text: '🏠 Самостоятельная работа (фриланс)', value: '1' },
          { text: '🏢 Работа в компании', value: '23' },
        ],
      },
      {
        question: 'Какая сфера тебя больше привлекает? 🌐',
        options: [
          { text: '🎨 Разработка веб-сайтов', value: '1' },
          { text: '⚙️ Разработка серверной логики', value: '2' },
          { text: '📊 Анализ данных', value: '3' },
        ],
      },
      {
        question: 'Какую работу ты бы выбрал? 💡',
        options: [
          { text: '✨ Создание красивых и удобных сайтов', value: '1' },
          { text: '📈 Анализ больших данных', value: '3' },
          { text: '🔧 Оптимизация серверов и автоматизация', value: '2' },
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
          ? '🎨 Вам подходит Frontend! Вы сможете создавать красивые и удобные веб-сайты, работать с HTML, CSS и JavaScript. Frontend-разработчики отвечают за внешний вид и взаимодействие с пользователем.'
          : maxCategory === '2'
            ? '⚙️ Вам подходит Backend! Вы будете работать с серверной частью приложений, базами данных и бизнес-логикой. Backend-разработчики обеспечивают надежную работу систем и их масштабируемость.'
            : '📊 Вам подходит Анализ данных! Вы сможете работать с большими массивами информации, выявлять закономерности и помогать бизнесу принимать решения на основе данных. Data-аналитики используют статистику, машинное обучение и визуализацию.'
    }

    const restartQuiz = () => {
      currentQuestionIndex.value = 0
      answers.value = []
      showResult.value = false
      resultText.value = ''
    }

    return { questions, currentQuestionIndex, showResult, resultText, handleAnswer, restartQuiz }
  },
}
</script>

<style>
body {
  font-family: 'Segoe UI', Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  min-height: 100vh;
}

#app {
  max-width: 1000px;
  margin: 0 auto;
  background: transparent;
  border-radius: 0 0 20px 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  overflow-x: hidden;
}

.site-header {
  background: linear-gradient(45deg, #1976d2, #388e3c);
  padding: 15px 0;
  margin-bottom: 30px;
  position: sticky;
  top: 0;
  z-index: 1000;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 95%;
  margin: 0 auto;
  padding: 0 20px;
}

.logo {
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.1);
}

h1 {
  font-size: clamp(1.8rem, 5vw, 2.8rem);
  margin: 25px 0;
  padding: 0 25px;
  background: linear-gradient(45deg, #1976d2, #388e3c);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

@media (max-width: 480px) {
  body {
    padding: 0;
  }

  #app {
    border-radius: 0;
  }

  .header-content {
    flex-direction: column;
    gap: 15px;
    padding: 10px;
  }

  .nav-links {
    font-size: 0.95rem;
    gap: 15px;
  }

  .nav-link {
    padding: 6px 12px;
  }

  h1 {
    font-size: 1.8rem;
    margin: 20px 0;
  }
}
</style>
