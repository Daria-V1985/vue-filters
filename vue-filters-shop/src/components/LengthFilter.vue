<template>
  <div class="content-item__container">
    <Length  
      v-for="length in lengths"
      :key="length.id"
      :item="length.item"
      :value="length" 
      @change="onChange"
    />
  </div>
</template>

<script >
import Length from "@/components/Length.vue";

export default {
  name: "LengthFilter",
  components: {
    Length,
  },
  props: {
    lengths: Array,
  },
    data() {
    return {
      selectedLengths: [],
    };
  },
  methods: {
    onChange({ value, checked }) {
      if (checked) {
        this.selectedLengths.push(value);
      } else {
        this.selectedLengths = this.selectedLengths.filter(b => b !== value);
      }
      this.$emit('change', this.selectedLengths);
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