<script setup>
import { ref, watch } from 'vue';
const question = ref('');
const finalAnswer = ref(null)
const bgUrl = ref(null)
const isValidQuestion = ref(false)
watch(question, (question, oldQuestion) => {
  isValidQuestion.value = false
  if (!question.endsWith('?')) return
  isValidQuestion.value = true
  getAnswer();

}
)
const getAnswer = async () => {
  finalAnswer.value = 'Thinking...'
  const { answer, image } = await fetch('https://yesno.wtf/api')
    .then(r => r.json())
  finalAnswer.value = answer.toUpperCase();
  bgUrl.value = image;

}
</script>
<template>
  <img v-if="bgUrl" :src="bgUrl" :alt="finalAnswer" />
  <div class="bg-dark"></div>
  <div class="indecision-container">
    <input v-model.trim="question" type="text" placeholder="Please, make a question" />
    <p v-show="!isValidQuestion">Don't forget to use a question mark at the end of your Question (?)</p>
    <div v-if="isValidQuestion">
      <h2>{{ question }}</h2>
      <h1>{{ finalAnswer }}</h1>
    </div>
  </div>
</template>
<style scoped>
img,
.bg-dark {
  height: 100vh;
  left: 0px;
  max-height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0px;
  width: 100vw;
}

.bg-dark {
  background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
  position: relative;
  z-index: 99;
}

input {
  width: 250px;
  padding: 10px 15px;
  border-radius: 5px;
  border: none;
  margin-bottom: 50px;
  text-align: center;
}

input:focus {
  outline: none;
}

p {
  color: white;
  font-size: 20px;
  margin-top: 0px;
}

h1,
h2 {
  color: white;
}

h2 {
  margin-top: 150px;
}
</style>