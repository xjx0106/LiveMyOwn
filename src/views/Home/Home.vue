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
          {{ data.title }}
        </div>
      </div>
      <div class="mian-right">
        <div class="header">
          <div
            v-for="(item, index) in data.header"
            :key="index"
            class="items"
            @click="jumpToItem(index)"
          >
            <div class="title">
              {{ item.title }}
            </div>
            <div class="item-img">
              <img :src="item.poster" alt="" @load="imageLoad(item.title)" />
            </div>
            <div class="introduce" :style="introduceStyle">
              {{ item.introduce }}
            </div>
          </div>
        </div>
      </div>
    </div>
    <Loading v-if="loadingShow" class="loading" :style="loadingStyle"></Loading>
  </div>
</template>

<script>
import ee from "@/components/eventEmitter.js";
import dataConfig from "@/assets/file/data.js";
import Loading from "@/components/Loading.vue";

export default {
  name: "Home",
  components: {
    Loading
  },
  data() {
    return {
      loadingShow: true,
      loadingStyle: "opacity: 1",
      data: null,
      imageCompleteWatcher: {
        // 九龍城寨: false,
        // 霓虹消逝: false,
        // 網路潔癖: false,
        // bg: false
      },
      introduceStyle: "" // 介紹的文字的動態樣式
    };
  },
  created() {
    console.log("home created");
    this.data = dataConfig;
    this.initImageCompleteWatcher();
  },
  mounted() {
    console.log("home mounted");
  },
  watch: {
    imageCompleteWatcher: {
      handler(val) {
        console.log("【watch】imageCompleteWatcher", JSON.stringify(val));
        let value = JSON.parse(JSON.stringify(val));

        this.$nextTick(() => {
          let allowHideLoading = true;
          let finishedCount = 0;
          Object.values(value).forEach(isThisPicLoaded => {
            if (isThisPicLoaded === false) {
              allowHideLoading = false;
            } else {
              finishedCount++;
            }
          });
          ee.emit("setProgress", finishedCount, Object.values(value).length);
          if (!allowHideLoading) {
            console.log("【watch】存在未加載完成的圖片...");
          } else {
            console.log("【watch】全部圖片已經加載！");
            console.log("【watch】全部圖片已經加載，請求關閉loading頁面！");
            setTimeout(() => {
              this.introduceStyle = "z-index: 9999";
              this.loadingStyle = "opacity: 0";
            }, 300);
            setTimeout(() => {
              console.log("【watch】執行loading消失");
              this.loadingShow = false;
            }, 1300);
          }
        });
      },
      deep: true
      // immediate: true,
    }
  },
  computed: {},
  beforeDestroy() {
    this.introduceStyle = "";
  },
  methods: {
    /**
     * 跳轉到項目
     */
    jumpToItem(item) {
      console.log("jump", item);
      if (item === "0") {
        this.$router.push("/Kowloon-Walled-City");
      }
    },
    /**
     * 旋轉加載消失
     */
    // loadingDisappear() {
    //   console.log("收到loading消失的請求");
    //   this.loadingStyle = "opacity: 0";
    //   setTimeout(() => {
    //     this.loadingShow = false;
    //     console.log("執行loading消失");
    //   }, 1100);
    // },
    /**
     * 初始化圖片集合
     * @description 用於通過watch檢測圖片是否已經全部加載完畢
     */
    initImageCompleteWatcher() {
      dataConfig.header.forEach(itme => {
        this.imageCompleteWatcher[itme.title] = false;
      });
      this.imageCompleteWatcher.bg = false;
      this.imageCompleteWatcher = JSON.parse(
        JSON.stringify(this.imageCompleteWatcher)
      );
      // console.log(this.imageCompleteWatcher);
    },
    /**
     * 背景視頻（背景圖片）加載完畢
     */
    backgroundLoaded() {
      // console.log("img", "bg");
      this.imageCompleteWatcher.bg = true;
      // console.log(this.imageCompleteWatcher);
    },
    /**
     * 列表的圖片加載完畢
     * @param {String} p 圖片的名字
     */
    imageLoad(p) {
      // console.log("img", p);
      this.imageCompleteWatcher[p] = true;
      // console.log(this.imageCompleteWatcher);
    }
  }
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

          .title {
            width: 30%;
            font-size: 20px;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
          }
          .introduce {
            transition: opacity 0.6s;
            margin-left: 20px;
            margin-right: 20px;
            width: 70%;
            font-size: 16px;
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
              // filter: blur(2px);
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
        .items:hover .item-img > img {
          transform: scale(1.2);
        }
        .items:hover .introduce {
          color: white;
          opacity: 0.6;
        }
      }
    }
  }
  .loading {
    transition: all 1s;
  }
}
</style>
