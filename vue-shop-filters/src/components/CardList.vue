<template>

  <div class="catalog__products products">
    <div class="products__card">
      <TheCard 
      v-for="item in items"
      :key = "item.id"
      :category = "item.category"
      :title = "item.title" 
      :image-url = "item.imageUrl"
      :price = "item.price"
      :color = "item.color"
      />
    </div>
  </div>

</template>

<script setup>
  import TheCard from '../components/TheCard.vue';

  defineProps ({
    items: Array
  })
</script>