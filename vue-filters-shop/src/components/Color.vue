<template>
  <div class="content-item__border">
    <div class="content-item__color" :style="'background-color:' + background"></div>
  </div>
</template>

<script>
export default {
  props: {
    background: String,
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  &__border {
    width: 27px;
    height: 27px;
    border: 1px solid transparent;
    transition: border 0.1s ease;
    position: relative;
    &:hover,
    &.active {
      border: 2px solid $mainColorOne;
      transition: border 0.1s ease;
    }
  }
  &__color {
    width: 17px;
    height: 17px;
    cursor: pointer;
    position: absolute;
    top: 48%;
    left: 49%;
    transform: translate(-50%, -50%);
  }
}
</style>