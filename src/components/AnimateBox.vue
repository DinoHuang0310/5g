<template>
  <div
    id="animate-box"
    class="area"
  >
    <video autoplay loop muted playsinline :style="{'transform': setScale()}">
      <source src="../assets/images/media.mp4" type="video/mp4" />
    </video>
    <Introduction
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="0"
    >
      <p><span>台灣邁入5G元年</span></p>
    </Introduction>
    <Introduction
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="0.5"
    >
      <p><span>投資機會全面引爆</span></p>
    </Introduction>
    <div class="scroll-down">
      <div />
    </div>
  </div>
</template>

<script>
import Introduction from './Introduction.vue'
export default {
  components: {
    Introduction
  },
  props: {
    scrollTop: {
      type: Number,
      required: true
    },
    windowHeight: {
      type: Number,
      required: true
    },
  },
  methods: {
    setScale() {
      const offset = this.windowHeight * 2;
      if(this.scrollTop > offset && this.scrollTop < (this.windowHeight * 3)) {
        const percentage = 1.5 / (this.windowHeight);
        return `translate(-50%, -50%) scale(${(this.scrollTop - offset) * percentage + 1})`;
      }
    }
  }
}
</script>

<style>
#animate-box {
  padding: 5%;
  background: black;
}
.scroll-down {
  position: absolute;
  width: 100%;
  height: 20%;
  bottom: 0;
  left: 0;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0) 0%, rgba(0, 0, 0, .7) 100%);
}
.scroll-down div {
  position: absolute;
  width: 30px;
  height: 55px;
  left: 50%;
  bottom: 1.5em;
  margin-left: -15px;
  border: solid 2px white;
  border-radius: 15px;
}
.scroll-down div:before {
  content: '';
  position: absolute;
  width: 4px;
  height: 9px;
  top: 8px;
  left: 11px;
  border-radius: 2px;
  background: white;
  -webkit-animation-name: scrollDown;
  animation-name: scrollDown;
  animation-iteration-count: infinite;
  animation-duration: 1.5s;
}
video {
  position: absolute;
  top: 50%;
  left: 50%;
  min-width: 100%;
  min-height: 100%;
  width: auto;
  height: auto;
  transform: translate(-50%, -50%);
  background-image: url("../assets/images/media-background.png");
  background-position: center;
  background-size: cover;
  opacity: .7;
}
@keyframes scrollDown {
  from {
    transform: translate(0, 0);
  }
  to {
    transform: translate(0, 10px);
  }
}
</style>
