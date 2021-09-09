<template>
  <div class="loading-modal">
    <div class="loading">
      <div class="logo">
        <img src="@/assets/image/loading.gif" />
      </div>
      <div class="text">L o a d i n g {{ dots }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Loading",
  data() {
    return {
      dots: "",
    };
  },
  created() {
    let dotCount = 0;
    setInterval(() => {
      this.setDot(dotCount);
      if(dotCount === 3) {
        dotCount = 0;
      } else {
        dotCount++;
      }
    }, 1000);
  },
  mounted() {},
  methods: {
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
    }
  },
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
  }
}
</style>
