<template>
  <div class="content-item__container">
    <Brand  
      v-for="brand in brands"
      :key="brand.id"
      :name="brand.name"
      :value="brand" 
      :checked="modelValue.includes(brand.id)"
      @change="checked => onBrandChange({ id: brand.id, checked })"
    />
  </div>
</template>

<script lang="js">
import { onMounted } from "vue";
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
  data() {
    return {
      selectedBrands: [],
    };
  },
  methods: {
    onBrandChange({ id, checked }) {
      let updated = [...this.modelValue];
      if (checked) {
        if (!updated.includes(id)) {
          updated.push(id);
        }
      } else {
        updated = updated.filter(bid => bid !== id);
      }
      this.$emit('update:modelValue', updated);
      console.log('ID фильтров получены:', JSON.parse(JSON.stringify(updated)));
    },
  },
  emits: ['update:modelValue'],
  setup(props) {
    onMounted(() => {
      console.log('BrandFilter - Initial modelValue:', props.modelValue);
    });

    const updateValue = (value) => {
      console.log('BrandFilter - Emitting update:modelValue', value);
      this.$emit('update:modelValue', value); 
    };

    return {
      updateValue
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
}
</style>