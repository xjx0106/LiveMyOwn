<template>
  <div class="home">
    <div class="background">
      <video
        type="video/mp4"
        loop
        class="video"
        muted
        @canplay="backgroundLoaded"
        ref="video"
        autobuffer
        autoplay
        playsinline
      >
        <source src="@/assets/video/neon-bg2.mp4" />
      </video>
      <!-- <img
        @load="backgroundLoaded"
        autobuffer
        class="video"
        src="../assets/image/neon-bg2.gif"
      /> -->
    </div>
    <div class="mian-area">
      <div class="mian-left">
        <div class="mian-title">
          標題標題標題
        </div>
      </div>
      <div class="mian-right"></div>
    </div>
  </div>
</template>

<script>
import ee from "@/components/eventEmitter.js";
export default {
  name: "Home",
  data() {
    return {};
  },
  created() {},
  computed: {},
  methods: {
    async backgroundLoaded() {
      // alert("ready to emit")
      console.log("backgroundLoaded, emit home-loaded");
      ee.emit("home-loaded");
      this.$nextTick(() => {
        this.$refs.video.play();
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  background-color: black;
  .background {
    position: fixed;
    height: 100%;
    width: 100%;
    // filter: blur(4px);
    .video {
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
  }
  .mian-area {
    // z-index: 1;
    color: white;
    font-size: 40px;
    height: 100%;
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    .mian-left {
      // border: 1px solid red;
      height: 93%;
      width: 47%;
      background-color: #00000000;
      display: flex;
      align-items: center;
      .mian-title {
        text-align: center;
        color: white;
        width: 100%;
        font-size: 54px;
        // border: 1px solid red;
        height: fit-content;
      }
    }
    .mian-right {
      height: 93%;
      width: 47%;
      background-color: #00000066;
    }
    > div {
      width: 50px;
      height: 50px;
    }
  }
}
</style>
