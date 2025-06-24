<template>
  <div class="content-item__container">
    <Brand  
      v-for="brand in brands"
      :key="brand.id"
      :name="brand.name"
      :value="brand" 
      v-model="selectedBrandsMap[brand.name]"
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
  emits: ['update:modelValue'],
  data() {
    return {
      selectedBrandsMap: {},
      internalUpdate: false,
    };
  },
  watch: {
    modelValue: {
      immediate: true,
      handler(newVal) {
        if (this.internalUpdate) {
          this.internalUpdate = false;
          return;
        }
        const map = {};
        this.brands.forEach(brand => {
          map[brand.name] = newVal.includes(brand.name);
        });
        this.selectedBrandsMap = map;
      }
    },
    selectedBrandsMap: {
      deep: true,
      handler(newArr) {
        this.internalUpdate = true;
        const selected = Object.keys(newArr).filter(name => newArr[name]);
        this.$emit('update:modelValue', selected);
      }
    }
  },
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