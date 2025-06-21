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

function onFilter(filters) {
  console.log('Применённые фильтры:', JSON.parse(JSON.stringify(filters)));
  filteredItems.value = items.value.filter(item => {
    console.log('Проверяем товар:', item);
    if (filters.brand && filters.brand.length > 0) {
      if (!filters.brand.includes(item.brand)) {
        console.log('Типы фильтра и товара:', typeof filters.brand[0], typeof item.brand);
        console.log('Отсекаем по бренду', item.brand);
        return false;
      }
    }
    if (filters.size && filters.size.length > 0) {
      if (!filters.size.includes(item.size)) {
        console.log('Типы фильтра и товара:', typeof filters.size[0], typeof item.size);
        console.log('Отсекаем по размеру', item.size);
        return false;
      }
    }
    if (filters.length && filters.length.length > 0) {
      if (!filters.length.includes(item.length)) {
        console.log('Типы фильтра и товара:', typeof filters.length[0], typeof item.length);
        console.log('Отсекаем по длине платья', item.length);
        return false;
      }
    }
    if (filters.color && filters.color.length > 0) {
      if (!filters.color.includes(item.color)) {
        console.log('Отсекаем по цвету', item.color);
        return false;
      }
    }
    if (filters.priceRange) {
      const [minPrice, maxPrice] = filters.priceRange;
      if (item.price < minPrice || item.price > maxPrice) {
        console.log('Отсекаем по цене', item.price);
        return false;
      }
    }
    return true;
  });
  console.log('Отфильтрованные товары:', filteredItems.value);
}

</script>
