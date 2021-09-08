<template>
  <div class="home">
    <div
      class="background"
      :style="{ backgroundImage: 'url(' + backgroundImageUrl + ')' }"
    ></div>
    <div class="text">home page</div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      backgroundImageUrl: require("../assets/image/bg4.jpg"),
    };
  },
  created() {
    let bgCount = 1;
    setInterval(() => {
      this.setBackground(bgCount);
      if (bgCount === 4) {
        bgCount = 1;
      } else {
        bgCount++;
      }
    }, 15000);
  },
  computed: {},
  methods: {
    setBackground(bgCount) {
      if(bgCount === 1) {
        this.backgroundImageUrl = require("../assets/image/bg1.jpg");
      }
      if(bgCount === 2) {
        this.backgroundImageUrl = require("../assets/image/bg2.jpg");
      }
      if(bgCount === 3) {
        this.backgroundImageUrl = require("../assets/image/bg3.jpg");
      }
      if(bgCount === 4) {
        this.backgroundImageUrl = require("../assets/image/bg4.jpg");
      }
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
    position: absolute;
    top: 0px;
    left: 0px;
    height: 100%;
    width: 100%;
    z-index: 1;
    background-size: cover;
    transition: background-image 6s;
    filter: blur(4px);
  }
  .text {
    color: white;
    font-size: 40px;
    padding-top: 40px;
  }
}
</style>
