<template>
  <div class="catalog__filters filter-catalog">
    <div class="filter-catalog__items">
      <div class="filter-catalog__item">
        <div class="filter-catalog__item-title">brand</div>
        <BrandFilter :brands="brands" />
      </div>
      <div class="filter-catalog__item">
        <div class="filter-catalog__item-title">size (Inches)</div>
        <SizeFilter :sizes="sizes" />
      </div>
      <div class="filter-catalog__item">
        <div class="filter-catalog__item-title">dress length</div>
        <LengthFilter :lengths="lengths" />
      </div>
      <div class="filter-catalog__item">
        <div class="filter-catalog__item-title">color</div>
        <ColorFilter :colors="colors" />
      </div>
      <div class="filter-catalog__item">
        <div class="filter-catalog__item-title">price Range</div>
        <PriceFilter />
      </div>
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

import { onMounted, ref } from "vue";
import axios from "axios";

const sizes = ref([]);
const colors = ref([]);
const brands = ref([]);
const lengths = ref([]);

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://ba8e5ca6f7d01757.mokky.dev/sizes",
    );
    sizes.value = data;
  } catch (error) {
    console.log(error);
  }
});

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://ba8e5ca6f7d01757.mokky.dev/colors"
    );
    colors.value = data;
  } catch (error) {
    console.log(error);
  }
});

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://ba8e5ca6f7d01757.mokky.dev/brands"
    );
    brands.value = data;
  } catch (error) {
    console.log(error);
  }
});

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://ba8e5ca6f7d01757.mokky.dev/lengths"
    );
    lengths.value = data;
  } catch (error) {
    console.log(error);
  }
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

  .filter-catalog {
  min-width: 355px;
  &__items {
    font-family: $mainFont;
    font-size: 14px;
  }
  &__item {
    margin-bottom: 60px;
    position: relative;
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