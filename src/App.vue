<template>
  <div id="app">
    <router-view :key="this.$route.path" />
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {};
  }
};
</script>

<style lang="scss" scoped>
#app {
  position: absolute;
  left: 0px;
  top: 0px;
  height: 100%;
  width: 100%;

  background-color: black;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  overflow: hidden; // 阻止手機滑動
  position: fixed; // 阻止手機滑動
}
</style>
