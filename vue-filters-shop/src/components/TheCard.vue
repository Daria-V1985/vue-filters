<template>
  <article class="products__card-item card-item">
    <a href="#" class="card-item__img">
      <img :src="imageUrl" alt="Card product" />
    </a>
    <div class="card-item__info">
      <div class="card-item__category">{{ category }}</div>
      <div class="card-item__title">{{ title }}</div>
      <div class="card-item__price">{{ price }} eur</div>
      <div class="card-item__colors">
        <div class="card-item__border">
          <div class="card-item__color" :style="'background:' + color"></div>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  props: {
    imageUrl: String,
    category: String,
    title: String,
    price: Number,
    color: String,
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.card-item {
  font-family: $dopFont;
  display: flex;
  flex-direction: column;
  gap: 5px;
  border-radius: 5px;
  transition: box-shadow 0.25s ease;
  &:hover {
    box-shadow: 0px 4px 6px rgba($colorOne, 0.3);
    transition: box-shadow 0.25s ease;
  }
  &__img {
    display: block;
    width: 330px;
    height: auto;
    img {
      max-width: 100%;
      border-radius: 5px;
    }
  }
  &__info {
    padding: 5px 0 15px 15px;
  }
  &__category {
    font-size: 12px;
    font-weight: 600;
    color: $mainColorThree;
    text-transform: uppercase;
  }
  &__title {
    font-size: 18px;
    font-weight: 400;
  }
  &__price {
    font-size: 22px;
    font-weight: 500;
    text-transform: uppercase;
  }
  &__colors {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  &__border {
    width: 27px;
    height: 27px;
    border: 1px solid transparent;
    transition: border 0.1s ease;
    position: relative;
    &:hover,
    &.active {
      border: 2px solid $mainColorOne;
      transition: border 0.1s ease;
    }
  }
  &__color {
    width: 17px;
    height: 17px;
    cursor: pointer;
    position: absolute;
    top: 48%;
    left: 49%;
    transform: translate(-50%, -50%);
  }
}
</style>