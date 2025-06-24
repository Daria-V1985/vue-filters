<template>
  <div class="catalog__filters filter-catalog">
    <div class="filter-catalog__items">
      <Accordion v-model:selectedFilters="filters" />
    </div>
    <button 
      class="filter-catalog__btn"
      @click="filterCards">
      apply
    </button>
  </div>
</template>

<script>
import Accordion from "@/components/Accordion.vue";
import { ref, watch } from "vue";

export default {
  name: "FiltersList",
  components: {
    Accordion,
  },
  props: {
    brands: Array,
  },
  emits: ['filter'],
  setup(props, { emit }) {
    const filters = ref({
      brand: [],
      size: [],
      length: [],
      color: [],
      priceRange: [0, 100],
    });

    watch(filters, (newVal) => {
      console.log('selectedFilters changed:', JSON.parse(JSON.stringify(newVal)));
    }, { deep: true });

    function filterCards() {
      console.log('Нажата кнопка Apply');
      emit('filter', filters.value);
    }

    return {
      filters,
      filterCards,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.filter-catalog {
  min-width: 355px;
  &__items {
    font-family: $mainFont;
    font-size: 14px;
  }
  &__btn {
    text-transform: uppercase;
    background: #F0F2F2;
    color: #828282;
    padding: 10px 30px;
    outline: none;
    border: 2px solid #828282;
    font-size: 14px;
    font-weight: 500;
    line-height: 21px;
    letter-spacing: 0.5px;
    text-align: center;
    margin-left: 65%;
    cursor: pointer;
  }
}

</style>