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
      <div class="mian-right">
        <div class="header">
          <div v-for="(item, index) in data.header" :key="index" class="items">
            <div class="title">
              {{item.title}}
            </div>
            <div class="item-img">
              <img :src="item.poster" alt="" >
            </div>
            <div class="introduce">
              {{item.introduce}}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ee from "@/components/eventEmitter.js";
import dataEnglish from "@/assets/file/data.js"
export default {
  name: "Home",
  data() {
    return {
      data: null
    };
  },
  created() {
    this.data = dataEnglish;
  },
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
      height: 95%;
      width: 47.5%;
      // background-color: red;
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
      height: 95%;
      width: 47.5%;
      background-color: #00000066;
      .header {
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        cursor: pointer;
        .items {
          border: 1px solid #ffffff00;
          transition: all 0.3s;
          display: flex;
          flex-direction: row;
          height: 100%;
          position: relative;
          
          .title{ 
            width: 30%;
            font-size: 20px;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
          }
          .introduce {
            width: 70%;
            font-size: 20px;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
          }
          .item-img {
            transition: opacity 0.6s;
            opacity: 0;
            height: 100%;
            width: 70%;
            position: absolute;
            right: 0px;
            overflow: hidden;
            > img {
              filter: blur(2px);
              transition: transform 0.6s;
              transform: scale(1);
              height: 100%;
              width: 100%;
            }
          }
        }
        .items:hover {
          border: 1px solid #ffffff88;
          background-color: black;
        }
        .items:hover .item-img {
          overflow: hidden;
          opacity: 1;
        }
        .items:hover .item-img >img {
          transform: scale(1.2);
        }
        .items:hover .introduce {
          z-index: 9999;
          color: white;
        }
      }
    }
  }
}
</style>
