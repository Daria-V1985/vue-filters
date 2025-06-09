<template>
  <div class="content-item__container">
    <Brand  
      v-for="brand in brands"
      :key="brand.id"
      :name="brand.name"
      :value="brand" 
      @change="onBrandChange"
    />
  </div>
</template>

<script lang="js">
import Brand from "@/components/Brand.vue";

export default {
  name: "BrandFilter",
  components: {
    Brand,
  },
  props: {
    brands: Array,
    value: Object,
  },
  data() {
    return {
      selectedBrands: [],
    };
  },
  methods: {
    onBrandChange({ value, checked }) {
      if (checked) {
        this.selectedBrands.push(value);
      } else {
        this.selectedBrands = this.selectedBrands.filter(b => b !== value);
      }
      this.$emit('change', this.selectedBrands);
    },
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
}
</style>