<template>
  <HomeView />
  <router-view />
</template>

<script>
import HomeView from "./views/HomeView.vue";

export default {
  name: "app",
  components: {
    HomeView,
  }
}

</script>

<style lang="scss">

</style>