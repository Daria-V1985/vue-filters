<template>
    <div class="content-item__checkbox checkbox">
      <input 
        :id="value.name" 
        class="checkbox__input" 
        type="checkbox" 
        :value="value" 
        :checked="modelValue"
        @change="onChange"
      />
      <label :for="value.name" class="checkbox__label">{{ value.name }}</label>
    </div>
</template>

<script  lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    name: {
      type: String,
    },
    value: {
      type: Object,
      required: true,
    },
    modelValue: {
      type: Boolean,
      required: true,
    },
  },
  emits: ['update:modelValue'],
  methods: {
    onChange(event: Event) {
      const target = event.target as HTMLInputElement;
      this.$emit( 'update:modelValue', target.checked );
    },
  },
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.checkbox {
  &__input {
    display: none;
    margin-right: 9px;
    &:checked + .checkbox__label:after {
      transform: scale(1);
      transition: all 0.5s ease;
    }
  }
  &__label {
    width: 100%;
    display: inline-flex;
    align-items: center;
    flex-wrap: nowrap;
    cursor: pointer;
    position: relative;
    transition: all 0.25s ease;
    &:before {
      font-size: 16px;
      content: '';
      align-self: start;
      flex: 0 0 15px;
      height: 15px;
      background-color: transparent;
      border: 1px solid $mainColorThree;
      margin: 3px 12px 0 0;
    }
    &:after {
      content: '\2713';
      width: 16px;
      height: 16px;
      font-size: 18px;
      position: absolute;
      top: 3px;
      left: 0;
      color: $mainColorThree;
      background-color: $mainColorOne;
      transform: scale(0);
      transition: all 0.5s ease;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }
}
</style>