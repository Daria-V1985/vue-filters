<template>
    <div class="filter-catalog__item-content content-item">
      <div class="content-item__container">
        <Brand  
          v-for="brand in brands"
          :key="brand.id"
          :name="brand.name"
        />
      </div>
    </div>
</template>

<script>
import Brand from "@/components/Brand.vue";

export default {
  name: "BrandFilter",
  components: {
    Brand,
  },
  props: {
    brands: Array,
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