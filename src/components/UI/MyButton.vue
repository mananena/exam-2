<template>
  <button class="button" @click="handleButton" :type="isSubmit ? 'submit' : '' ">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button',
  props: {
    isSubmit: Boolean,
    handleButton: {
      type: Function,
      default: null
    }
  }
};
</script>

<style scoped lang="scss">
@use '@/assets/scss/function' as *;
@use '@/assets/scss/variables' as *;
@use '@/assets/scss/mixin' as *;

.button {
  padding: 10px;
  color: color(secondDescColor);
  background-color: color(primaryTitleColor);
  border: 1px solid color(primaryTitleColor);
  border-radius: 30px;
  transition: all .3s ease;
  @include media(min, md) {
    padding: 15px;
  }
  &:focus {
    box-shadow: 0px 0px 7px 3px #757575;
  }
  &:active {
    background-color: #00aaff;
  }
}
</style>
