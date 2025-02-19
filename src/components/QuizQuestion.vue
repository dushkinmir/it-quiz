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
}

/* Светлая тема */
@media (prefers-color-scheme: light) {
  .question-block {
    background-color: #f8f9fa;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .question {
    color: #2c3e50;
  }

  .option label {
    background-color: white;
    border: 2px solid #e9ecef;
    color: #2c3e50;
  }

  .option label:hover {
    border-color: #4caf50;
    background-color: #f1f8f1;
  }
}

/* Темная тема */
@media (prefers-color-scheme: dark) {
  .question-block {
    background-color: #1a1a1a;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }

  .question {
    color: #ffffff;
  }

  .option label {
    background-color: #2c2c2c;
    border: 2px solid #3a3a3a;
    color: #ffffff;
  }

  .option label:hover {
    border-color: #4caf50;
    background-color: #333333;
  }
}

.question {
  font-size: clamp(1rem, 4vw, 1.25rem);
  margin-bottom: 20px;
  font-weight: 600;
  padding: 0 10px;
}

.option {
  display: block;
  margin: 12px 0;
  padding: 0 5px;
}

.option label {
  display: flex;
  align-items: center;
  padding: clamp(8px, 2vw, 12px) clamp(12px, 3vw, 16px);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: clamp(0.9rem, 3vw, 1rem);
  word-break: break-word;
}

.option input[type='radio'] {
  margin-right: 12px;
  min-width: 18px;
  min-height: 18px;
  accent-color: #4caf50;
}

button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: clamp(10px, 2vw, 12px) clamp(20px, 4vw, 24px);
  border-radius: 6px;
  font-size: clamp(0.9rem, 3vw, 1rem);
  cursor: pointer;
  transition: background-color 0.2s ease;
  margin-top: 16px;
  width: 100%;
  max-width: 100%;
}

button:hover {
  background-color: #45a049;
}

button:active {
  transform: scale(0.98);
}

@media (max-width: 480px) {
  .question-block {
    margin: 10px auto;
  }

  .option {
    margin: 8px 0;
  }
}
</style>
