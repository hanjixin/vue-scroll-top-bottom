<template>
  <div class="movement" @click="goBottom()"></div>
</template>

<script>
export default {
  props: ["container", "speed"],
  name: "movement",
  data: function(params) {
    return {
      scrollHeight: 500,
      scrollTop: 0,
      defaulteSpeed: 30,
      nowSpeed: 100,
      defaultContainer: document.documentElement || document.body
    };
  },
  mounted() {
    this.speed ? (this.nowSpeed = this.defaulteSpeed = this.speed) : "";
    this.defaultContainer =
      document.querySelector(this.container) || this.defaultContainer;

    this.defaultContainer.addEventListener("scroll", this.handelScroll, false);
    this.defaultContainer.onload = () => {
      this.scrollHeight = this.defaultContainer.scrollHeight;
    };
    console.log(this.scrollHeight);
  },
  destroyed() {
    this.defaultContainer.removeEventListener(
      "scroll",
      this.handelScroll,
      false
    );
  },
  methods: {
    handelScroll() {
      this.scrollTop =
        this.defaultContainer.scrollTop ||
        window.pageYOffset ||
        this.defaultContainer.scrollTop;
      this.scrollHeight = this.defaultContainer.scrollHeight;
    },
    changeSpeed() {
      if (this.nowSpeed >= this.defaulteSpeed * 2.5) {
        this.nowSpeed = this.defaulteSpeed * 2.5;
      } else {
        this.nowSpeed = this.defaulteSpeed * 2;
      }
    },
    goBottom() {
      console.log("bottom");
      window.requestAnimationFrame = (function() {
        return (
          window.requestAnimationFrame ||
          window.webkitRequestAnimationFrame ||
          window.mozRequestAnimationFrame ||
          function(callback) {
            window.setTimeout(callback, 1000 / 60);
          }
        );
      })();
      var step =
        (this.scrollHeight -
          this.scrollTop / (this.defaulteSpeed / (1000 / 60))) <<
        0;

      console.log("bottom", step, this.scrollTop);
      var self = this;
      function fn() {
        // console.log(self.scrollTop, self.scrollTop, self.scrollHeight);
        if (self.scrollTop <= self.scrollHeight - window.innerHeight) {
          self.scrollTop += self.defaulteSpeed / (1000 / 60);
          self.defaultContainer.scrollTop = self.scrollTop;
          fn.rafTimer = requestAnimationFrame(fn);
        } else {
          self.defaultContainer.scrollTop = self.scrollHeight;
          cancelAnimationFrame(fn.rafTimer);
        }
      }

      fn.rafTimer = requestAnimationFrame(fn);
      fn();
    }
  }
};
</script>

<style scoped>
.movement {
  position: absolute;
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background: white;
  top: 400px;
  right: 20px;
  border: 5px solid #eeeeee;
  z-index: 999;
}
</style>
