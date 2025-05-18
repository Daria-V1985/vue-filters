<template>
  <section class="catalog">
          <div class="catalog__container">
            <div class="catalog__body">
              <FiltersList />
              <CardList :items="items"/>
            </div>
          </div>
        </section>
</template>

<script setup>
  import { onMounted, ref } from 'vue';
  import axios from 'axios';
  import CardList from './components/CardList.vue';
  import FiltersList from './components/FiltersList.vue';

  const items = ref([]);

  onMounted(async () => {
    try {
      const { data } = await axios.get('https://ba8e5ca6f7d01757.mokky.dev/cards');
      items.value = data;
    }
    catch (error) {
      console.log(error);
    }
  })
</script>