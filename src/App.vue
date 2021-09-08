<template>
  <div id="app">
    <Loading v-if="loadingShow" class="loading" :style="loadingStyle"></Loading>
    <Home></Home>
  </div>
</template>

<script>
import Loading from "./components/Loading.vue";
import Home from "./components/Home.vue";

export default {
  name: "App",
  components: {
    Loading,
    Home
  },
  data() {
    return {
      loadingShow: true,
      loadingStyle: "opacity: 1"
    }
  },
  created() {
    setTimeout(() => {
      this.loadingStyle = "opacity: 0";
    }, 3000);
    setTimeout(() => {
      this.loadingShow = false;
    }, 3100);
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

  background-color: white;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  // overflow: hidden;
  .loading {
    transition: all 1s;
  }
}
</style>
