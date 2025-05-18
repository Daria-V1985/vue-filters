<template>

  <article class="products__card-item card-item">
    <a href="#" class="card-item__img">
      <img :src="imageUrl" alt="Card product">
    </a>
    <div class="card-item__info">
      <div class="card-item__category">{{ category }}</div>
      <div class="card-item__title">{{ title }}</div>
      <div class="card-item__price">{{ price }} eur</div>
      <div class="card-item__colors">
        <div class="card-item__border">
          <div class="card-item__color" :class="color"></div>
        </div>
      </div>
    </div>
  </article>

</template>

<script setup>
  defineProps ({
    imageUrl: String,
    category: String,
    title: String,
    price: Number,
    color: String
  })
</script>