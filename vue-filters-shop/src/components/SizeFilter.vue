<template>
    <div class="filter-catalog__item-content content-item">
      <div class="content-item__container">
        <div class="content-item__sizes">
          <Size 
            v-for="size in sizes"
            :key="size.id"
            :name="size.name"
          />
        </div>
      </div>
    </div>
</template>

<script>
import Size from "@/components/Size.vue";

export default {
  name: "SizeFilter",
  components: {
    Size,
  },
  props: {
    sizes: Array,
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  text-transform: uppercase;
  overflow: hidden;
  //display: none;
  transition: all 0.25s ease;
  &__container {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
  &__sizes {
    width: 90%;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
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
  &__colors {
    width: 85%;
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
  }
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