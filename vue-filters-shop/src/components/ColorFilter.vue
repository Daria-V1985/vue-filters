<template>
  <div class="content-item__container">
    <div class="content-item__colors">
      <Color 
        v-for="color in colors"
        :key="color.id"
        :background="color.background"
        :value="color.background"
        v-model="selectedColors"
      />
    </div>
  </div>
</template>

<script >
import Color from "@/components/Color.vue";

export default {
  name: "ColorFilter",
  components: {
    Color,
  },
  props: {
    colors: {
      type: Array,
      required: true, 
    },
    modelValue: {
      type: Array,
      default: () => [], 
    },
  },
  data() {
    return {
      selectedColors: this.modelValue ? this.modelValue.slice() : [],
    };
  },
  watch: {
    selectedColors(newColors) {
      this.$emit('update:modelValue', newColors); 
    }
  },
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
  &__colors {
    width: 85%;
    display: flex;
    flex-wrap: wrap;
    gap: 14px;
  }
}
</style>