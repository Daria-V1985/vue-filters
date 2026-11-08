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

<script lang="ts">
import TheCard from "@/components/TheCard.vue";
import { defineComponent } from "vue";

interface Item {
  id: number,
  category: string,
  title: string,
  imageUrl: string,
  price: number,
  color: string
}

export default defineComponent({
  name: "CardList",
  components: {
    TheCard,
  },
  props: {
    items: {
      type: Array as () => Item[],  // поле, в котором указывается конструктор типа пропса: это массив элементов типа Item. Но чтобы Vue и TypeScript правильно поняли, что это массив объектов типа Item, нужно явно указать тип с помощью приведения типа (as).
      required: true,  // Говорит Vue, что компонент не сможет корректно работать без этого пропса. Пропс обязателен для передачи в компонент, Vue предупреждает при отсутствии.
    }
  }
});
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