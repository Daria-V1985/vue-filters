<template>
  <div class="content-item__container">
    <Length  
      v-for="length in lengths"
      :key="length.id"
      :item="length.name"
      :value="length" 
      :checked="modelValue.includes(length.name)"
      @change="checked => onLengthChange({ name: length.name, checked })"
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
    lengths: {
      type: Array,
      required: true
    },
    modelValue: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    onLengthChange({ name, checked }) {
      let updated = [...this.modelValue];
      if (checked) {
        if (!updated.includes(name)) {
          updated.push(name);
        }
      } else {
        updated = updated.filter(lname => lname !== name);
      }
      this.$emit('update:modelValue', updated);
      console.log('ID фильтров получены:', JSON.parse(JSON.stringify(updated)));
    },
  },
  emits: ['update:modelValue'],
  mounted() {
    console.log('LengthFilter - Initial modelValue:', this.modelValue);
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