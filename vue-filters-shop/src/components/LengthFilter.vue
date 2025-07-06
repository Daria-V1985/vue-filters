<template>
  <div class="content-item__container">
    <Length  
      v-for="length in lengths"
      :key="length.id"
      :item="length.name"
      :value="length" 
      v-model="selectedLengthsMap[length.name]"
    />
  </div>
</template>

<script lang="ts">
import Length from "@/components/Length.vue";
import { defineComponent } from "vue";

interface length {
  id: number,
  name: string,
  value: string,
}

export default defineComponent({
  name: "LengthFilter",
  components: {
    Length,
  },
  props: {
    lengths: {
      type: Array as () => length[],
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
      selectedLengthsMap: {} as Record<string, boolean>,
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
        const map: Record<string, boolean> = {};
        this.lengths.forEach(length => {
          map[length.name] = newVal.includes(length.name);
        });
        this.selectedLengthsMap = map;
      }
    },
    selectedLengthsMap: {
      deep: true,
      handler(newArr) {
        this.internalUpdate = true;
        const selected = Object.keys(newArr).filter(name => newArr[name]);
        this.$emit('update:modelValue', selected);
      }
    }
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
}
</style>