<script setup>
import { computed, watch } from "vue";
import Btn from "../shared/btn.vue";
const props = defineProps({
    results: Array,
});
defineEmits(["restart"]);
const meta = defineModel("meta", {
    type: Object,
});
const isRightCount = computed(() => {
    return props.results.filter((result) => result.answer.isCorrect).length;
});
const totalQuestions = computed(() => {
    return props.results.length;
});

if (isRightCount.value == 0) {
    meta.value.title = "Упс :(";
    meta.value.desc = "Вы неправильно ответили на все вопросы. Нужно подучить теорию.";
} else if (isRightCount.value == totalQuestions.value) {
    meta.value.title = "Поздравляем!";
    meta.value.desc =
        "Вы правильно ответили на все вопросы. Вы действительно отлично разбираетесь в IT";
} else {
    meta.value.title = "Хороший результат!";
    meta.value.desc = `Вы ответили правильно на ${isRightCount.value} вопросов. Так держать!`;
}
</script>
<template>
    <dl class="quiz-answers">
        <div v-for="result in results" class="quiz-answer-card"
            :class="{ 'is-right': result.answer.isCorrect, unright: !result.answer.isCorrect }">
            <dt class="quiz-answer-card__termin">{{ result.question }}</dt>
            <dd class="quiz-answer-card__description">
                {{ result.answer.text }}
            </dd>
        </div>
    </dl>
    <Btn @click="$emit('restart')" v-if="isRightCount !== totalQuestions" class="quiz-answers-reload">
        Пройти еще раз
    </Btn>
</template>
<style lang="scss">
@import "#/vars.scss";

.quiz-answers-reload {
    margin-top: 40px;
    margin-left: auto;
    margin-right: auto;
}

.quiz-answers {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.quiz-answer-card {
    padding: 40px;
    display: flex;
    flex-direction: column;
    gap: 15px;
    border-radius: $baseBorderRadius;

    &__termin {
        font-size: 20px;
        font-weight: 700;
    }

    &.unright {
        background-color: $red;
    }

    &.is-right {
        background-color: $green;
    }
}
</style>
