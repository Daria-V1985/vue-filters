<template>
  <div class="content-item__size" @click="toggleActive" :class="{ active: isActive }">{{ name }}</div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

export default defineComponent({
  props: {
    name: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },        
    modelValue: {
      type: Array as PropType<any>,
      required: true, 
    },
  },
  computed: {
    isActive(): boolean {
      return this.modelValue.includes(this.value); 
    },
  },
  methods: {
    toggleActive() {
      if (this.value === undefined || this.value === null) {
        return;
      }
      let newValue = [...this.modelValue];
      if (this.isActive) {
        newValue = newValue.filter(size => size !== this.value); 
      } else {
        newValue.push(this.value); 
      }
      this.$emit('update:modelValue', newValue); 
    },
  },
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  &__size {
    width: 46px;
    height: 46px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: $mainColorThree;
    border: 1px solid $mainColorThree;
    cursor: pointer;
    transition: border 0.1s ease;
    &:hover,
    &.active {
      color: $mainColorOne;
      border: 2px solid $mainColorOne;
      transition: border 0.1s ease;
    }
  }
}
</style>