<template>
    <button class="btn">
        <slot />
    </button>
</template>
<style lang="scss">
@import "#/vars.scss";

.btn {
    font-size: 18px;
    background-color: $blue;
    padding: 16px 31px;
    text-align: center;
    border-radius: 10px;
    color: $white;
    font-weight: 700;
    display: block;
    width: fit-content;
    cursor: pointer;
}
</style>
