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
}
</style>