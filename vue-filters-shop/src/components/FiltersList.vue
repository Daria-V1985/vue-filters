<template>
  <div class="catalog__filters filter-catalog">
    <div class="filter-catalog__items">
      <Accordion title="Brand" v-model="brandOpen">
        <BrandFilter v-model:modelValue="filters.brand" :brands="brands"/>
      </Accordion>

      <Accordion title="Size (Inches)" v-model="sizeOpen">
        <SizeFilter v-model:modelValue="filters.size" :sizes="sizes"/>
      </Accordion>

      <Accordion title="Dress Length" v-model="lengthOpen">
        <LengthFilter v-model:modelValue="filters.length" :lengths="lengths"/>
      </Accordion>

      <Accordion title="Color" v-model="colorOpen">
        <ColorFilter v-model:modelValue="filters.color" :colors="colors"/>
      </Accordion>

      <Accordion title="Price Range" v-model="priceOpen">
        <PriceFilter v-model:modelValue="filters.priceRange" :min="minPrice" :max="maxPrice"/>
      </Accordion>
    </div>
    <button 
      class="filter-catalog__btn"
      @click="filterCards">
      apply
    </button>
  </div>
</template>

<script lang="ts">
import Accordion from "@/components/Accordion.vue";
import BrandFilter from '@/components/BrandFilter.vue';
import SizeFilter from '@/components/SizeFilter.vue';
import LengthFilter from '@/components/LengthFilter.vue';
import ColorFilter from '@/components/ColorFilter.vue';
import PriceFilter from '@/components/PriceFilter.vue';
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";

interface brand {
  id: number,
  name: string,
  value: string,
}

interface size {
  id:number,
  name: string,
  value: string,
}

interface length {
  id: number,
  name: string,
  value: string,
}

interface color {
  id: number,
  background: string,
  value: string,
}

export default defineComponent({
  name: "FiltersList",
  components: {
    Accordion,
    BrandFilter,
    SizeFilter,
    LengthFilter,
    ColorFilter,
    PriceFilter,
  },
  emits: ['filter'],
  setup(_, { emit }) {
  
    const brands = ref<brand[]>([]);
    const sizes = ref<size[]>([]);
    const lengths = ref<length[]>([]);
    const colors = ref<color[]>([]);
    const minPrice = ref(0);
    const maxPrice = ref(100);

    const filters = ref({
      brand: [] as string[],
      size: [] as string[],
      length: [] as string[],
      color: [] as string[],
      priceRange: [minPrice.value, maxPrice.value] as [number, number],
    });

    const brandOpen = ref(false);
    const sizeOpen = ref(false);
    const lengthOpen = ref(false);
    const colorOpen = ref(false);
    const priceOpen = ref(false);

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

    function filterCards() {
      emit('filter', filters.value);
    }

    return {
      brands,
      sizes,
      lengths,
      colors,
      minPrice,
      maxPrice,
      filters,
      brandOpen,
      sizeOpen,
      lengthOpen,
      colorOpen,
      priceOpen,
      filterCards,
    };
  },
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