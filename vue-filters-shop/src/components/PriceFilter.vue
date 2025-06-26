<template>
  <div class="content-item__container">
    <div class="content-item__price price-filter">
      <div class="price-filter__slider">
        <span class="price-filter__range min">0.00 eur</span>
        <span class="price-filter__range max">100.00 eur</span>
        <Slider v-model="value" class="price-filter__track track" />
      </div>
    </div>
  </div>
</template>

<script>
import Slider from '@vueform/slider';

export default {
  name: "PriceFilter",
  components: { 
    Slider 
  },
  props: {
    modelValue: {
      type: Array,
      default: () => [0, 100]
    }
  },
  emits: ['update:modelValue'],
  computed: {
    value: {
      get() {
        return this.modelValue;
      },
      set(val) {
        this.$emit('update:modelValue', val);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  &__container {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
}

.price-filter {
	&__slider {
    width: 100%;
    position: relative;
    cursor: pointer;
    height: 0.5rem;
    margin-top: 30px;
	}
  &__range {
    position: absolute;
    top: -2rem;
    &.min {
      left: 0;
    }
    &.max {
      right: 34px;
    }
	}
}

.track {
  background-color: $mainColorThree;
  display: block;
  position: absolute;
  width: 90%;
  height: 0.2rem;
	&__highlight {
    background-color: $mainColorOne;
    display: block;
    position: absolute;
    width: 90%;
    height: 0.2rem;
    z-index: 2;
	}
	&__btn {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    outline: none;
    cursor: pointer;
    display: block;
    position: absolute;
    z-index: 2;
    width: 6px;
    height: 20px;
    top: calc(-50% - 0.25rem);
    border: none;
    background-color: $mainColorOne;
    -ms-touch-action: pan-x;
    touch-action: pan-x;
    transition: box-shadow .3s ease-out,background-color .3s ease,-webkit-transform .3s ease-out;
    transition: transform .3s ease-out,box-shadow .3s ease-out,background-color .3s ease;
    transition: transform .3s ease-out,box-shadow .3s ease-out,background-color .3s ease,-webkit-transform .3s ease-out;
	}
}
</style>