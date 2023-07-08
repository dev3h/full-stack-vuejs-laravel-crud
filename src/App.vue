<template>
  <HeaderNav title="Dev3h CRUD" />
  <router-view></router-view>
</template>

<script>
import HeaderNav from "./components/Header.vue";
export default {
  name: "App",
  components: {
    HeaderNav,
  },
};
</script>

<style></style>
