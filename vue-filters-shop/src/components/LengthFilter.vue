<template>
    <div class="filter-catalog__item-content content-item">
      <div class="content-item__container">
        <Length  
          v-for="length in lengths"
          :key="length.id"
          :item="length.item"
        />
      </div>
    </div>
</template>

<script>
import Length from "@/components/Length.vue";

export default {
  name: "LengthFilter",
  components: {
    Length,
  },
  props: {
    lengths: Array,
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
}
</style>