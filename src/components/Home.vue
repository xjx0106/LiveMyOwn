<template>
  <div class="home">
    <div class="background">
      <video src="@/assets/video/neon-bg.mp4" type="video/mp4" autoplay loop class="video" muted @canplay="videoLoaded" ref="video"/>
    </div>
    <div class="text">home page</div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {

    };
  },
  created() {

  },
  computed: {},
  methods: {
    videoLoaded() {
      console.log("videoLoaded");
      // this.$refs.video.play();
    }
  },
};
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  background-color: black;
  .background {
    position: absolute;
    top: 0px;
    left: 0px;
    height: 100%;
    width: 100%;
    // z-index: 1;
    // background-size: cover;
    // transition: background-image 6s;
    // filter: blur(4px);
    .video {
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
  }
  .text {
    color: white;
    font-size: 40px;
    padding-top: 40px;
  }
}
</style>
