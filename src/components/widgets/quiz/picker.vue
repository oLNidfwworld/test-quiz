<script setup>
import RadioInput from "@/components/shared/radio-input.vue";
import { watch, ref } from "vue";
const props = defineProps({
  answers: Array,
  currentQuestion: Number,
});

const emits = defineEmits(["onAnswer"]);

const answer = ref();
const isInert = ref(false);

watch(answer, (newVal) => {
  if (typeof newVal === "number") {
    isInert.value = true;
    setTimeout(() => {
      emits("onAnswer", newVal);
      answer.value = undefined;
      isInert.value = false;
    }, 1000);
  }
});
</script>
<template>
  <div class="quiz-view-pick">
    <RadioInput :inert="isInert" v-model="answer" v-for="(answers, index) in answers"
      :key="`${currentQuestion}_${answers.id}`" :value="answers.id" :id="`${currentQuestion}_${answers.id}`"
      name="questions">
      {{ answers.text }}
    </RadioInput>
  </div>
</template>
<style lang="scss">
.quiz-view-pick {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
