<template>
  <div class="catalog__filters filter-catalog">
    <div class="filter-catalog__items">
      <BrandFilter />
      <SizeFilter />
      <LengthFilter />
      <ColorFilter />
      <PriceFilter />
    </div>
    <button class="filter-catalog__btn disabled">apply</button>
  </div>
</template>

<script setup>
import BrandFilter from "@/components/BrandFilter.vue";
import ColorFilter from "@/components/ColorFilter.vue";
import LengthFilter from "@/components/LengthFilter.vue";
import PriceFilter from "@/components/PriceFilter.vue";
import SizeFilter from "@/components/SizeFilter.vue";
</script>
