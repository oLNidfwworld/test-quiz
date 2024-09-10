<script setup>
import BaseHeader from "./components/widgets/base-header.vue";
import Quiz from "./components/widgets/quiz";
import QuizResults from "./components/widgets/quiz-results.vue";
import { data } from "./assets/mock/questions.json";
import { shallowRef, ref, reactive } from "vue";
import shuffle from "./composables/shuffle";

const megaShuffle = () => {
  const _unshffledData = [...data];
  _unshffledData.forEach((data, i) => {
    _unshffledData[i].answers = shuffle(data.answers);
  });
  return shuffle(_unshffledData);
};

const allQuestions = shallowRef(megaShuffle());
const currentStep = ref(0);
const answers = shallowRef({});
const results = shallowRef([]);
const isFullFilled = ref(false);

const meta = reactive({
  title: "Тестирование",
  desc: "",
});

const fullfillResults = (event) => {
  const _results = [];
  for (let i in event) {
    const questionObject = allQuestions.value.find(
      (question) => question.id === parseInt(i)
    );
    const answerObject = questionObject.answers.find(
      (answ) => answ.id === parseInt(event[i])
    );

    if (questionObject) {
      _results.push({
        question: questionObject.question,
        answer: answerObject,
      });
    }
  }
  results.value = _results;
  isFullFilled.value = true;
};
const restart = () => {
  isFullFilled.value = false;
  answers.value = {};
  currentStep.value = 0;
  allQuestions.value = megaShuffle();
  meta.title = "Тестирование";
  meta.desc = "";
};
</script>
<template>
  <div class="app-wrapper">
    <BaseHeader :meta="meta" />
    <main class="app-content">
      <Quiz v-if="!isFullFilled" v-model:answers="answers" v-model:currentStep="currentStep" :questions="allQuestions"
        @on-complete="fullfillResults" />
      <QuizResults v-else v-model:meta="meta" @restart="restart" :results="results" />
    </main>
  </div>
</template>
<style lang="scss" scoped>
.app-wrapper {
  max-width: 886px;
  margin: auto;
  padding-top: 82px;
  padding-bottom: 85px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}
</style>
