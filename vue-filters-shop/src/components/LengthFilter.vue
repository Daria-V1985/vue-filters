<template>
  <div class="content-item__container">
    <Length  
      v-for="length in lengths"
      :key="length.id"
      :item="length.item"
    />
  </div>
</template>

<script>
import Length from "@/components/Length.vue";

export default {
  name: "LengthFilter",
  components: {
    Length,
  },
  props: {
    lengths: Array,
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