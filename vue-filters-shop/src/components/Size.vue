<template>
  <div class="content-item__size" @click="toggleActive" :class="{ active: isActive }">{{ name }}</div>
</template>

<script>
export default {
  props: {
    name: String,
  },
    data() {
    return {
      isActive: false,
    };
  },
  methods: {
    toggleActive() {
      this.isActive = !this.isActive;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  &__size {
    width: 46px;
    height: 46px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: $mainColorThree;
    border: 1px solid $mainColorThree;
    cursor: pointer;
    transition: border 0.1s ease;
    &:hover,
    &.active {
      color: $mainColorOne;
      border: 2px solid $mainColorOne;
      transition: border 0.1s ease;
    }
  }
}
</style>