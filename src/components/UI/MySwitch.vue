<template>
  <label class="switch">
    <span class="visually-hidden">Переключатель</span>
    <input
      type="checkbox"
      :checked="checked"
      @input="updateCheck"
      class="visually-hidden"
    />
    <span class="switch__selector"></span>
  </label>
</template>

<script>
export default {
  name: 'my-switch',
  props: {
    checked: Boolean,
  },
  methods: {
    updateCheck() {
      this.$emit('check');
    },
  },
};
</script>

<style scoped lang="scss">
@use '@/assets/scss/function' as *;
@use '@/assets/scss/variables' as *;
@use '@/assets/scss/mixin' as *;
.switch__selector {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch__selector {
  cursor: pointer;
  background-color: #ccc;
  transition: 0.4s;
  border-radius: 34px;
}

.switch__selector:before {
  position: absolute;
  content: '';
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: 0.4s;
  border-radius: 50%;
}

input:checked + .switch__selector {
  background-color: color(primaryTitleColor);
}

input:focus + .switch__selector {
  outline: 3px solid navy;
}

input:checked + .switch__selector:before {
  transform: translateX(26px);
}
</style>
