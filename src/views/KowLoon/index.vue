<template>
  <div class="mian-pic" @mousemove="mouseMove">
    <img
      src="@/assets/image/kowloon-single-tall-building.jpg"
      alt=""
      class="tall-building"
      :style="moveTop"
    />
  </div>
</template>

<script>
export default {
  name: "Kowloon",
  data() {
    return {
      moveDirection: "",
      moveTop: "top: -20%"
    };
  },
  created() {
    console.log(window.innerHeight);
  },
  watch: {
    moveDirection: {
      handler() {
        console.log();
      }
    }
  },
  mounted() {},
  methods: {
    /**
     * 移動鼠標的方法
     * @param {Object} e 鼠標移動的參數
     */
    mouseMove(e) {
      // console.log(e.clientY);
      let percentageOfMoveArea = 0.2;
      if (e.clientY / window.innerHeight < percentageOfMoveArea) {
        console.log("up");
      } else if (e.clientY / window.innerHeight + percentageOfMoveArea > 1) {
        console.log("down");
      } else {
        console.log("stop");
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.mian-pic {
  height: 100%;
  width: 100%;
  position: relative;
  .tall-building {
    width: 100%;
    height: 340%;
    position: absolute;
    left: 0px;
    top: 0%;
  }
}
</style>
