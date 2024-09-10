<script setup>
defineProps({
  meta: Object,
});
</script>
<template>
  <header class="header">
    <div class="header__wrapper">
      <h1 class="header__title">{{ meta?.title }}</h1>
    </div>
    <span v-if="meta.desc" class="header__desc">
      {{ meta?.desc }}
    </span>
  </header>
</template>
<style scoped lang="scss">
@import "#/vars.scss";

.header {
  flex: 0 0 auto;
  margin-bottom: 20px;

  &__wrapper {
    display: flex;
    justify-content: space-between;
  }

  &__title {
    color: $black;
    font-size: 48px;
    font-weight: 800;
  }

  &__desc {
    display: block;
    margin-top: 20px;
    font-size: 24px;
  }
}
</style>
