<template>
  <div class="filter-catalog__item" :class="{ active: isOpen }"
  >
    <div @click="toggle" class="filter-catalog__item-title" :class="{ active: isOpen }">
      <slot name="title">{{ title }}</slot>
    </div>
    <div v-show="isOpen" class="filter-catalog__item-content content-item">
      <slot />
    </div>
  </div>
</template>

<script  lang="ts">
import { ref, watch, defineComponent } from "vue";

export default defineComponent({
  name: "Accordion",
  props: {
    title: {
      type: String,
      required: true
    },
    modelValue: {
      type: Boolean,
      default: false,
    }
  },
  emits: ['update:modelValue'],
  setup(props, { emit }) {
    const isOpen = ref(props.modelValue);

    watch(() => props.modelValue, (bool) => {
      isOpen.value = bool;
    });

    function toggle() {
      isOpen.value = !isOpen.value;
      emit('update:modelValue', isOpen.value)
    }

    return {
      toggle,
      isOpen,
    }
  },
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.filter-catalog {
  &__item {
    margin-bottom: 60px;
    position: relative;
    cursor: pointer;
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
}

.content-item {
  text-transform: uppercase;
  overflow: hidden;
  transition: all 0.25s ease;
}

</style>