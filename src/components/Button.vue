<template>
  <button @click="onClick" class="button">
    Create rule
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    onClick: {
      type: Function,
      required: true
    }
  }
}
</script>

<style scoped lang="scss">
@import "../styles/main.scss";

.button {
    width: 100px;
    height: 30px;
    margin: 0 auto;
    color: $button-primary-font-color;
    background: $button-primary-color;
    border: none;
    cursor: pointer;
}
</style>
