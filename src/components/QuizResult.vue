<template>
  <div class="result-container">
    <h2>Результат</h2>
    <p class="result">{{ result }}</p>
  </div>
</template>

<script>
export default {
  name: 'QuizResult',
  props: ['result'],
}
</script>

<style>
.result-container {
  max-width: 600px;
  width: 100%;
  margin: 20px auto;
  text-align: center;
  transition: all 0.3s ease;
  padding: 0 15px;
  box-sizing: border-box;
}

/* Светлая тема */
@media (prefers-color-scheme: light) {
  .result-container h2 {
    color: #2c3e50;
  }

  .result {
    background-color: #f8f9fa;
    color: #4caf50;
    border: 2px solid #4caf50;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
}

/* Темная тема */
@media (prefers-color-scheme: dark) {
  .result-container h2 {
    color: #ffffff;
  }

  .result {
    background-color: #1a1a1a;
    color: #4caf50;
    border: 2px solid #4caf50;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
  }
}

.result-container h2 {
  font-size: clamp(1.5rem, 5vw, 2rem);
  margin-bottom: 20px;
}

.result {
  font-size: clamp(1.2rem, 4vw, 1.5rem);
  font-weight: bold;
  padding: clamp(15px, 3vw, 20px);
  margin: 20px 0;
  border-radius: 12px;
  transition: all 0.3s ease;
  word-wrap: break-word;
}

@media (max-width: 480px) {
  .result-container {
    margin: 10px auto;
  }

  .result {
    margin: 10px 0;
  }
}
</style>
