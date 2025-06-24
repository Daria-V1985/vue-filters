<template>
  <div class="content-item__container">
    <Brand  
      v-for="brand in brands"
      :key="brand.id"
      :name="brand.name"
      :value="brand" 
      :checked="modelValue.includes(brand.name)"
      @change="checked => onBrandChange({ name: brand.name, checked })"
    />
  </div>
</template>

<script>
import Brand from "@/components/Brand.vue";

export default {
  name: "BrandFilter",
  components: {
    Brand,
  },
  props: {
    brands: {
      type: Array,
      required: true
    },
    modelValue: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    onBrandChange({ name, checked }) {
      let updated = [...this.modelValue];
      if (checked) {
        if (!updated.includes(name)) {
          updated.push(name);
        }
      } else {
        updated = updated.filter(bname => bname !== name);
      }
      this.$emit('update:modelValue', updated);
      console.log('ID фильтров получены:', JSON.parse(JSON.stringify(updated)));
    },
  },
  emits: ['update:modelValue'],
  mounted() {
    console.log('BrandFilter - Initial modelValue (names):', this.modelValue);
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
</style>