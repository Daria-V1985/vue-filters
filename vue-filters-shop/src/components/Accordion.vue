<template>
  <div 
    v-for="(item, index) in filterItems" 
    :key="index" 
    class="filter-catalog__item"
    :class="{ active: isOpen(index) }"
  >
    <div
      @click="toggle(index)"
      class="filter-catalog__item-title" 
      :class="{ active: isOpen(index) }">
      {{ item.title }}
    </div>
    <div v-show="isOpen(index)" class="filter-catalog__item-content content-item">
      <component :is="item.component" v-bind="item.props" />
    </div>
  </div>
</template>

<script>
import BrandFilter from '@/components/BrandFilter.vue'
import SizeFilter from '@/components/SizeFilter.vue'
import LengthFilter from '@/components/LengthFilter.vue'
import ColorFilter from '@/components/ColorFilter.vue'
import PriceFilter from '@/components/PriceFilter.vue'

import { onMounted, ref } from "vue";
import axios from "axios";

export default {
  name: "Accordion",
  components: {
    BrandFilter,
    SizeFilter,
    LengthFilter,
    ColorFilter,
    PriceFilter,
  },
  setup() {

    const sizes = ref([]);
    const colors = ref([]);
    const brands = ref([]);
    const lengths = ref([]);

    onMounted(async () => {
      try {
        const [brandsResponce, sizesResponce, colorsResponce, lengthsResponce] = await Promise.all([
          axios.get("https://ba8e5ca6f7d01757.mokky.dev/brands"),
          axios.get("https://ba8e5ca6f7d01757.mokky.dev/sizes"),
          axios.get("https://ba8e5ca6f7d01757.mokky.dev/colors"),
          axios.get("https://ba8e5ca6f7d01757.mokky.dev/lengths"),
        ]);
        brands.value = brandsResponce.data;
        sizes.value = sizesResponce.data;
        colors.value = colorsResponce.data;
        lengths.value = lengthsResponce.data;
      } catch (error) {
        console.log(error);
      }
    });

    const openAccordion = ref([]);

    const filterItems = ref([
      { title: 'Brand', component: 'BrandFilter', props: { brands } },
      { title: 'Size (Inches)', component: 'SizeFilter', props: { sizes } },
      { title: 'Dress Length', component: 'LengthFilter', props: { lengths } },
      { title: 'Color', component: 'ColorFilter', props: { colors } },
      { title: 'Price Range', component: 'PriceFilter', props: {} },
    ]);

    function toggle(index) {
      if (openAccordion.value.includes(index)) {
        openAccordion.value = openAccordion.value.filter(i => i !== index)
      } else {
        openAccordion.value.push(index)
      }
    }

    function isOpen(index) {
      return openAccordion.value.includes(index)
    }

    return {
      filterItems,
      toggle,
      isOpen,
    }
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.filter-catalog {
  &__item {
    margin-bottom: 60px;
    position: relative;
    cursor: pointer;
    &-title {
      font-family: $dopFont;
      font-size: 24px;
      text-transform: capitalize;
      margin-bottom: 25px;
      &:after,
      &:before {
        content: '';
        width: 14px;
        height: 2px;
        background-color: $mainColorTwo;
        position: absolute;
        right: 2%;
        margin-top: 18px;
        transition: transform 0.15s ease;
      }
      &:after { 
        transform: rotate(-90deg);
      }
    }
    &.active {
      .filter-catalog__item-title:after {
        transform: rotate(0deg);
        transition: transform 0.15s ease;
      }
      .content-item {
        display: block;
        animation: visible 1s forwards;
      }
    }
  }
}

.content-item {
  text-transform: uppercase;
  overflow: hidden;
  transition: all 0.25s ease;
}

</style>