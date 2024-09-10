<script setup>
import Picker from "./picker.vue";
import ProgressBar from "../../shared/progress-bar.vue";
import { computed, shallowReactive, ref } from "vue";

const { questions } = defineProps({
  questions: {
    type: Array,
    default: [],
  },
});
const emits = defineEmits(["onComplete"]);

const answers = defineModel("answers", {
  type: Object,
});
const currentStep = defineModel("currentStep", {
  type: Number,
});
const currentStepQuestions = computed(() => questions[currentStep.value]);
const totalQuestion = computed(() => questions.length);

const saveAndNext = (e) => {
  answers.value[currentStepQuestions.value.id] = e;
  if (!(currentStep.value < totalQuestion.value - 1)) {
    emits("onComplete", answers.value);
    return;
  }
  currentStep.value++;
};
</script>
<template>
  <div class="quiz-view">
    <div class="quiz-view__content">
      <span class="quiz-view__title">
        {{ questions[currentStep].question }}
      </span>
      <Picker @on-answer="saveAndNext" :current-question="currentStep" :answers="currentStepQuestions.answers" />
    </div>

    <ProgressBar :currentIndex="currentStep + 1" :length="totalQuestion + 1" />
  </div>
</template>
<style lang="scss">
@import "#/vars.scss";

.quiz-view {
  &__content {
    padding: 40px;
    background: $gray;
    border-radius: $baseBorderRadius;
  }

  &__title {
    display: block;
    font-size: 24px;
    font-weight: 700;
    line-height: 1.219;
    margin-bottom: 20px;
  }
}
</style>
