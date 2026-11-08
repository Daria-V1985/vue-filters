<template>
    <div class="products__card">
      <TheCard
        v-for="item in items"
        :key="item.id"
        :category="item.category"
        :title="item.title"
        :imageUrl="item.imageUrl"
        :price="item.price"
        :color="item.color"
      />
    </div>
</template>

<script>
import TheCard from "@/components/TheCard.vue";

export default {
  name: "CardList",
  components: {
    TheCard,
  },
  props: {
    items: Array,
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.products {
  &__card {
    display: grid;
    grid-template-columns: repeat(3, auto);
    justify-content: space-between;
    column-gap: 20px;
    row-gap: 35px;
  }
}
</style>