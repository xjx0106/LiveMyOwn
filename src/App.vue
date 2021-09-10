<template>
  <div id="app">
    <Home></Home>
    <Loading v-if="loadingShow" class="loading" :style="loadingStyle"></Loading>
  </div>
</template>

<script>
import Loading from "@/components/Loading.vue";
import Home from "@/components/Home.vue";
import ee from "@/components/eventEmitter.js";

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
    ee.on("home-loaded", this.loadingDisappear);
  },
  beforeDestroy() {
    ee.off("home-loaded", this.loadingDisappear);
  },
  methods: {
    loadingDisappear() {
      console.log("收到loading消失的請求");
      this.loadingStyle = "opacity: 0";
      setTimeout(() => {
        this.loadingShow = false;
        console.log("執行loading消失");
      }, 1100);
    }
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
  position:fixed; // 阻止手機滑動
  .loading {
    transition: all 1s;
  }
}
</style>
