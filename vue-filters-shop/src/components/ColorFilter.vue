<template>
    <div class="filter-catalog__item-content content-item">
      <div class="content-item__container">
        <div class="content-item__colors">
          <Color 
            v-for="color in colors"
            :key="color.id"
            :background="color.background"
          />
        </div>
      </div>
    </div>
</template>

<script >
import Color from "@/components/Color.vue";

export default {
  name: "ColorFilter",
  components: {
    Color,
  },
  props: {
    colors: Array,
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
  &__colors {
    width: 85%;
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
  }
}
</style>