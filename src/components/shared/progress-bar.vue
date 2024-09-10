<script setup>
const props = defineProps({
    length: Number,
    currentIndex: Number,
});
</script>
<template>
    <div class="progress">
        <div class="progress__digits">
            <span> 0 </span>
            <span>
                {{ length }}
            </span>
        </div>
        <div class="progress__bar">
            <div :style="{ width: `${(currentIndex / length) * 100}%` }" class="progress__progression" />
        </div>
        <span class="progress__current" :style="{ left: `${((currentIndex + 1) / length) * 100 - 10.5}%` }">{{
            currentIndex }}</span>
    </div>
</template>
<style lang="scss">
@import "#/vars.scss";

.progress {
    margin-top: 20px;
    width: 100%;
    position: relative;
    // height: 12px;

    &__digits {
        display: flex;
        font-weight: 700;
        justify-content: space-between;
        width: 100%;
    }

    &__bar {
        height: 12px;
        background: $gray;
        border-radius: 99px;
        margin-top: 3px;
        overflow: hidden;
    }

    &__progression {
        height: 100%;
        background: $blue;
        transition: width 0.5s ease-in-out;
        border-radius: 99px;
    }

    &__current {
        position: absolute;
        font-weight: 700;
        transition: 0.5s ease-in-out inset;
        bottom: -20px;
    }
}
</style>
