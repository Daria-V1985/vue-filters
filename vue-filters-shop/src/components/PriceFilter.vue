<template>
  <div class="filter-catalog__item">
    <div class="filter-catalog__item-title">price Range</div>
    <div class="filter-catalog__item-content content-item">
      <div class="content-item__container">
        <div class="content-item__price price-filter">
          <div class="price-filter__slider">
            <span class="price-filter__range min">0.00 eur</span>
            <span class="price-filter__range max">100.00 eur</span>
            <Slider v-model="value" class="price-filter__track track" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Slider from '@vueform/slider';

export default {
  name: "PriceFilter",
  components: { 
    Slider 
  },
  data: () => ({
    value: [10, 90]
  }),
};
</script>