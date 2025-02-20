<template>
  <div class="quiz-result" :class="getResultClass">
    <div class="result-content">
      <h2>Ваш результат:</h2>
      <p v-html="result"></p>
      <button class="restart-btn" @click="$emit('restart')">Пройти тест заново</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QuizResult',
  props: {
    result: {
      type: String,
      required: true,
    },
  },
  computed: {
    getResultClass() {
      if (this.result.includes('Frontend')) return 'frontend-bg'
      if (this.result.includes('Backend')) return 'backend-bg'
      return 'data-bg'
    },
  },
}
</script>

<style>
.quiz-result {
  padding: 30px;
  border-radius: 15px;
  margin: 20px;
  min-height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-size: cover;
  background-position: center;
  position: relative;
  overflow: hidden;
  animation: fadeIn 1s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.quiz-result::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(5px);
  animation: blurFadeIn 1s ease-out;
}

@keyframes blurFadeIn {
  from {
    backdrop-filter: blur(0px);
    background: rgba(255, 255, 255, 0);
  }
  to {
    backdrop-filter: blur(5px);
    background: rgba(255, 255, 255, 0.7);
  }
}

.frontend-bg {
  background-image: url('/images/frontend-bg.jpg');
}

.backend-bg {
  background-image: url('/images/backend-bg.jpg');
}

.data-bg {
  background-image: url('/images/data-bg.jpg');
}

.result-content {
  position: relative;
  z-index: 1;
  text-align: center;
  max-width: 600px;
  padding: 30px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 15px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

h2 {
  color: #1976d2;
  font-size: 2rem;
  margin-bottom: 20px;
}

p {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 30px;
  color: #333;
}

.restart-btn {
  background: linear-gradient(45deg, #acacac 0%, #272727 100%);
  color: white;
  border: none;
  padding: 12px 25px;
  border-radius: 8px;
  font-size: 1.1rem;
  cursor: pointer;
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
}

.restart-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

@media (max-width: 480px) {
  .quiz-result {
    margin: 10px;
    padding: 15px;
  }

  .result-content {
    padding: 20px;
  }

  h2 {
    font-size: 1.5rem;
  }

  p {
    font-size: 1rem;
  }
}
</style>
