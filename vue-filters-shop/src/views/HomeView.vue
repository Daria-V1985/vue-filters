<template>
  <section class="catalog">
    <div class="catalog__container">
      <div class="catalog__body">
        <FiltersList 
          class="catalog__filters filter-catalog"
          @filter="onFilter" 
        />
        <CardList 
          class="catalog__products products" 
          :items="filteredItems" />
      </div>
    </div>
  </section>
  <router-view />
</template>

<script setup>
import CardList from "@/components/CardList.vue";
import FiltersList from "@/components/FiltersList.vue";

import { onMounted, ref } from "vue";
import axios from "axios";

const items = ref([]);
const filteredItems = ref([]);

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://ba8e5ca6f7d01757.mokky.dev/cards"
    );
    items.value = data;
    filteredItems.value = data;
  } catch (error) {
    console.log(error);
  }
});

function onFilter(selectedFilters) {
  filteredItems.value = items.value.filter(item => {
    if (selectedFilters.brand && selectedFilters.brand.length > 0) {
      if (!selectedFilters.brand.includes(item.brand)) return false;
    }
    if (selectedFilters.size && selectedFilters.size.length > 0) {
      if (!selectedFilters.size.includes(item.size)) return false;
    }
    if (selectedFilters.length && selectedFilters.length.length > 0) {
      if (!selectedFilters.length.includes(item.length)) return false;
    }
    if (selectedFilters.color && selectedFilters.color.length > 0) {
      if (!selectedFilters.color.includes(item.color)) return false;
    }
    if (selectedFilters.priceRange) {
      const [minPrice, maxPrice] = selectedFilters.priceRange;
      if (item.price < minPrice || item.price > maxPrice) return false;
    }
    return true;
  });
}

</script>
