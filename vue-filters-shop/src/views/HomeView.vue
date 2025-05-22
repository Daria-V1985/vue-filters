<template>
  <section class="catalog">
    <div class="catalog__container">
      <div class="catalog__body">
        <FiltersList class="catalog__filters filter-catalog" />
        <CardList class="catalog__products products" :items="items" />
      </div>
    </div>
  </section>
  <router-view />
</template>

<script setup>
// @ is an alias to /src

import CardList from "@/components/CardList.vue";
import FiltersList from "@/components/FiltersList.vue";

import { onMounted, ref } from "vue";
import axios from "axios";

const items = ref([]);

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://ba8e5ca6f7d01757.mokky.dev/cards"
    );
    items.value = data;
  } catch (error) {
    console.log(error);
  }
});

</script>
