<script setup>
defineOptions({
    inheritAttrs: false,
});

const model = defineModel({
    required: true,
});
</script>
<template>
    <label class="radio-inpt" :for="$attrs.id" :inert="$attrs.inert">
        <input v-model="model" type="radio" v-bind="$attrs" />
        <span class="radio-inpt__text">
            <slot />
        </span>
    </label>
</template>
<style lang="scss" scoped>
@import "#/vars.scss";

.radio-inpt {
    cursor: pointer;
    position: relative;
    display: flex;
    align-items: center;
    gap: 20px;
    line-height: 1.218;
    transition: 0.3s ease-out opacity;

    input[type="radio"] {
        position: absolute;
        left: 0px;
        z-index: -1;
    }

    &::before {
        display: block;
        flex-shrink: 0;
        content: "";
        border: 1px solid $black;
        border-radius: 99px;
        width: 20px;
        aspect-ratio: 1/1;
        transition: 0.3s ease-out border-color, 0.3s ease-out background-color;
    }

    &:has(input[type="radio"]:checked) {
        &::before {
            background-color: $blue;
            border-color: $blue;
        }
    }

    &[inert] {
        opacity: 0.5;
    }
}
</style>
