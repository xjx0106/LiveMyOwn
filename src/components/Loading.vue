<template>
  <div class="loading-modal">
    <div class="loading">
      <div class="logo">
        <img src="@/assets/image/loading.gif" />
      </div>
      <div class="text">L o a d i n g {{ dots }}</div>
      <div class="progress-bar">
        <div class="bar">
          <div class="bar-content" :style="progressStyle"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ee from "@/components/eventEmitter.js";
export default {
  name: "Loading",
  data() {
    return {
      dots: "",
      progressStyle: "style: width: 0%"
    };
  },
  created() {
    ee.on("setProgress", this.setProgress);
    let dotCount = 0;
    setInterval(() => {
      this.setDot(dotCount);
      if (dotCount === 3) {
        dotCount = 0;
      } else {
        dotCount++;
      }
    }, 400);
  },
  mounted() {},
  beforeDestroy() {
    ee.off("setProgress", this.setProgress);
  },
  methods: {
    /**
     * 設置Loading後面3個小圓點
     * @param {Number} dotCount 現在有幾個小圓點了
     */
    setDot(dotCount) {
      switch (dotCount) {
        case 0:
          this.dots = "";
          break;
        case 1:
          this.dots = ".";
          break;
        case 2:
          this.dots = ". .";
          break;
        case 3:
          this.dots = ". . .";
          break;
      }
    },
    /**
     * 設置進度條的進度
     * @param {Number} count 當前已經加載完的資源文件（圖片、視頻等）
     * @param {Number} all 所有資源文件的數量
     */
    setProgress(count, all) {
      let percentage = (count / all) * 100;
      this.progressStyle = "width: " + percentage + "%";
    }
  }
};
</script>

<style lang="scss" scoped>
.loading-modal {
  position: absolute;
  left: 0px;
  top: 0px;
  height: 100%;
  width: 100%;
  background-color: #ffefc3;
  .loading {
    margin: 0px auto;
    margin-top: 45vh;
    .logo {
      > img {
        width: 20px;
        height: 20px;
      }
    }
    .text {
      margin-top: 10px;
      font-size: 16px;
    }
    .progress-bar {
      .bar {
        margin: 0px auto;
        margin-top: 10px;
        border: 2px solid #00000044;
        height: 10px;
        width: 150px;
        position: relative;
        .bar-content {
          transition: width 0.2s;
          height: 100%;
          overflow: hidden;
          width: 0%;
          background-color: #00000099;
        }
      }
    }
  }
}
</style>
