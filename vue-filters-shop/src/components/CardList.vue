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
