<template>
  <div class="question-block">
    <p class="question">{{ question.question }}</p>
    <div v-for="(option, index) in question.options" :key="index" class="option">
      <label>
        <input type="radio" :value="option.value" v-model="selectedAnswer" />
        {{ option.text }}
      </label>
    </div>
    <button @click="submitAnswer">Далее</button>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'QuizQuestion',
  props: ['question'],
  emits: ['answer'],
  setup(props, { emit }) {
    const selectedAnswer = ref('')

    const submitAnswer = () => {
      if (!selectedAnswer.value) {
        alert('Пожалуйста, выберите вариант ответа.')
        return
      }
      emit('answer', selectedAnswer.value)
      selectedAnswer.value = ''
    }

    return { selectedAnswer, submitAnswer }
  },
}
</script>

<style>
.question-block {
  border-radius: 12px;
  padding: clamp(15px, 3vw, 24px);
  max-width: 600px;
  width: 100%;
  margin: 20px auto;
  transition: all 0.3s ease;
  box-sizing: border-box;
  background: rgba(255, 255, 255, 0.95);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.question {
  font-size: clamp(1.2rem, 4vw, 1.4rem);
  margin-bottom: 25px;
  font-weight: 600;
  padding: 0 10px;
  color: #2196f3;
}

.option {
  display: block;
  margin: 15px 0;
  padding: 0 5px;
  transform: scale(1);
  transition: transform 0.2s ease;
}

.option:hover {
  transform: scale(1.02);
}

.option label {
  display: flex;
  align-items: center;
  padding: clamp(12px, 2vw, 16px) clamp(16px, 3vw, 20px);
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: clamp(0.95rem, 3vw, 1.1rem);
  word-break: break-word;
  background: linear-gradient(to right, rgba(33, 150, 243, 0.1), rgba(76, 175, 80, 0.1));
  border: 2px solid transparent;
  position: relative;
  overflow: hidden;
}

.option label:hover {
  border-color: #2196f3;
  background: linear-gradient(to right, rgba(33, 150, 243, 0.2), rgba(76, 175, 80, 0.2));
}

.option input[type='radio'] {
  margin-right: 15px;
  min-width: 20px;
  min-height: 20px;
  accent-color: #2196f3;
}

button {
  background: linear-gradient(45deg, #2196f3, #4caf50);
  color: white;
  border: none;
  padding: clamp(12px, 2vw, 16px) clamp(24px, 4vw, 32px);
  border-radius: 12px;
  font-size: clamp(1rem, 3vw, 1.1rem);
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 25px;
  width: 100%;
  max-width: 100%;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  box-shadow: 0 4px 15px rgba(33, 150, 243, 0.3);
}

button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(33, 150, 243, 0.4);
}

button:active {
  transform: translateY(0);
}

@media (max-width: 480px) {
  .question-block {
    margin: 10px auto;
    padding: 15px;
  }
}
</style>
