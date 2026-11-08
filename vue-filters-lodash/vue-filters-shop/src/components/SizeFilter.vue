<template>
  <div class="content-item__container">
    <div class="content-item__sizes">
      <Size 
        v-for="size in sizes"
        :key="size.id"
        :name="size.name"
        :value="size.name"
        v-model="selectedSizes"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Size from "@/components/Size.vue";
import { defineComponent } from "vue";

interface size {
  id:number,
  name: string,
  value: string,
}

export default defineComponent({
  name: "SizeFilter",
  components: {
    Size,
  },
  props: {
    sizes: {
      type: Array as () => size[],
      required: true, 
    },
    modelValue: {
      type: Array,
      default: () => [], 
    },
  },
  data() {
    return {
      selectedSizes: this.modelValue ? this.modelValue.slice() : [],
    };
  },
  watch: {
    selectedSizes(newSizes) {
      if (JSON.stringify(newSizes) !== JSON.stringify(this.modelValue)) {
        this.$emit('update:modelValue', newSizes);
      }
    },
    modelValue(newSizes) {
      if (JSON.stringify(newSizes) !== JSON.stringify(this.selectedSizes)) {
        this.selectedSizes = newSizes.slice();
      }
    },
  },
});
</script>

<style lang="scss" scoped>
@import "../assets/scss/_variables.scss";

.content-item {
  &__container {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
  &__sizes {
    width: 90%;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
}
</style>