<template>
  <div class="content-item__container">
    <div class="content-item__sizes">
      <Size 
        v-for="size in sizes"
        :key="size.id"
        :name="size.name"
        @change="onChange"
      />
    </div>
  </div>
</template>

<script>
import Size from "@/components/Size.vue";

export default {
  name: "SizeFilter",
  components: {
    Size,
  },
  props: {
    sizes: Array,
  },
    data() {
    return {
      selectedSizes: [],
    };
  },
  methods: {
    onChange(event) {
      const sizeName = event.target.value;
      if (event.target.checked) {
        this.selectedSizes.push(sizeName);
      } else {
        this.selectedSizes = this.selectedSizes.filter(b => b !== sizeName);
      }
      this.$emit('change', this.selectedSizes);
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
  &__sizes {
    width: 90%;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
}
</style>