<template>
  <div>
    <swiper :options="swiperOption" ref="mySwiper" class="swiper-no-swiping">
      <!-- slides -->
      <swiper-slide>
        <div class="scroll-container">
          <img class="auto-img" src="/static/30year.jpg" alt>
          <img class="auto-img" src="/static/30year.jpg" alt>
          <vueToTop :container="'.scroll-container'"></vueToTop>
          <movement :container="'.scroll-container'"/>
        </div>
      </swiper-slide>

      <swiper-slide>I'm Slide 3</swiper-slide>
      <swiper-slide>I'm Slide 5</swiper-slide>

      <!-- Optional controls -->
    </swiper>
  </div>
</template>

<script>
import "swiper/dist/css/swiper.css";
import vueToTop from "./totop.vue";
import movement from "./movement.vue";
import { swiper, swiperSlide } from "vue-awesome-swiper";
export default {
  name: "index",
  components: {
    swiper,
    swiperSlide,
    vueToTop,
    movement
  },
  data: function(params) {
    return {
      swiperOption: {
        direction: "vertical",
        height: window.innerHeight,
        onlyExternal: true,
        allowSwipeToNext: false,
        allowSwipeToPre: false
      }
    };
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.swiper;
    }
  },
  methods: {},
  created() {},
  mounted() {}
};
</script>

<style>
.auto-img {
  width: 100%;
  height: auto;
}
.scroll-container {
  height: 100%;
  overflow: auto;
}
.swiper-wrapper {
  /* overflow: hidden; */
  /* position: absolute; */
}
</style>
