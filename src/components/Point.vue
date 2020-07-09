<template>
  <transition name="fade">
    <div
      v-if="showbox"
      class="area"
      id="point"
    >
      <svg
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        :viewBox="`0 0 ${windowWidth} ${windowHeight}`"
      >
        <g v-show="dotsLayer1">
          <path
            d="M15,0C6.8,0,0,6.8,0,15s6.8,15,15,15s15-6.8,15-15S23.3,0,15,0z M12.8,27.3l1.2-11h0.2c-0.7-0.3-1.1-1-1.1-1.8 c0-1.1,0.9-1.9,2-1.9s1.9,0.9,1.9,1.9c0,0.8-0.4,1.4-1.1,1.8H16l1.2,11H12.8z M17,17.9c1.2-0.7,2-1.9,2-3.4c0-2.2-1.8-4-4-4 s-4,1.8-4,4c0,1.5,0.8,2.7,1.9,3.4L12,19.7c-1.8-1.1-3-2.9-3-5.2c0-3.3,2.7-5.9,5.9-5.9c3.3,0,5.9,2.7,5.9,5.9c0,2.2-1.2,4.1-3,5.2 L17,17.9z M20,23.1l-1-1.7c2.4-1.3,4-3.9,4-6.9c0-4.4-3.5-8-7.9-8s-8,3.5-8,8c0,2.9,1.6,5.5,4,6.9l-1,1.7c-2.9-1.7-4.9-4.9-4.9-8.6 C5.1,9,9.5,4.6,15,4.6s9.9,4.4,9.9,9.9C24.9,18.2,23,21.4,20,23.1z"
            fill="#ffffff"
            v-for="(n, index) in windowWidth > 480 ? 15 : 7"
            :key="index"
            :style="{
              'transform': `translate(${getRandom(-20, windowWidth + 20)}px, ${getRandom(-10, windowHeight + 10)}px) scale(${getRandom(250, 2000, true)})`,
              'opacity': getRandom(100, 400, true)
            }"
          />
        </g>
        <g v-show="dotsLayer2">
          <path
            d="M15,0C6.8,0,0,6.8,0,15s6.8,15,15,15s15-6.8,15-15S23.3,0,15,0z M12.8,27.3l1.2-11h0.2c-0.7-0.3-1.1-1-1.1-1.8 c0-1.1,0.9-1.9,2-1.9s1.9,0.9,1.9,1.9c0,0.8-0.4,1.4-1.1,1.8H16l1.2,11H12.8z M17,17.9c1.2-0.7,2-1.9,2-3.4c0-2.2-1.8-4-4-4 s-4,1.8-4,4c0,1.5,0.8,2.7,1.9,3.4L12,19.7c-1.8-1.1-3-2.9-3-5.2c0-3.3,2.7-5.9,5.9-5.9c3.3,0,5.9,2.7,5.9,5.9c0,2.2-1.2,4.1-3,5.2 L17,17.9z M20,23.1l-1-1.7c2.4-1.3,4-3.9,4-6.9c0-4.4-3.5-8-7.9-8s-8,3.5-8,8c0,2.9,1.6,5.5,4,6.9l-1,1.7c-2.9-1.7-4.9-4.9-4.9-8.6 C5.1,9,9.5,4.6,15,4.6s9.9,4.4,9.9,9.9C24.9,18.2,23,21.4,20,23.1z"
            fill="#ffffff"
            v-for="(n, index) in windowWidth > 480 ? 20 : 10"
            :key="index"
            :style="{
              'transform': `translate(${getRandom(-20, windowWidth + 20)}px, ${getRandom(-10, windowHeight + 10)}px) scale(${getRandom(250, 2000, true)})`,
              'opacity': getRandom(100, 400, true)
            }"
          />
        </g>
        <g v-show="dotsLayer3">
          <path
            d="M15,0C6.8,0,0,6.8,0,15s6.8,15,15,15s15-6.8,15-15S23.3,0,15,0z M12.8,27.3l1.2-11h0.2c-0.7-0.3-1.1-1-1.1-1.8 c0-1.1,0.9-1.9,2-1.9s1.9,0.9,1.9,1.9c0,0.8-0.4,1.4-1.1,1.8H16l1.2,11H12.8z M17,17.9c1.2-0.7,2-1.9,2-3.4c0-2.2-1.8-4-4-4 s-4,1.8-4,4c0,1.5,0.8,2.7,1.9,3.4L12,19.7c-1.8-1.1-3-2.9-3-5.2c0-3.3,2.7-5.9,5.9-5.9c3.3,0,5.9,2.7,5.9,5.9c0,2.2-1.2,4.1-3,5.2 L17,17.9z M20,23.1l-1-1.7c2.4-1.3,4-3.9,4-6.9c0-4.4-3.5-8-7.9-8s-8,3.5-8,8c0,2.9,1.6,5.5,4,6.9l-1,1.7c-2.9-1.7-4.9-4.9-4.9-8.6 C5.1,9,9.5,4.6,15,4.6s9.9,4.4,9.9,9.9C24.9,18.2,23,21.4,20,23.1z"
            fill="#ffffff"
            v-for="(n, index) in windowWidth > 480 ? 30 : 15"
            :key="index"
            :style="{
              'transform': `translate(${getRandom(-20, windowWidth + 20)}px, ${getRandom(-10, windowHeight + 10)}px) scale(${getRandom(250, 2000, true)})`,
              'opacity': getRandom(100, 400, true)
            }"
          />
        </g>
      </svg>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    scrollTop: {
      type: Number,
      required: true
    },
    windowHeight: {
      type: Number,
      required: true
    },
    windowWidth: {
      type: Number,
      required: true
    },
    sectionIndex: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      showbox: false,
      // showDots: 0,
      dotsLayer1: false,
      dotsLayer2: false,
      dotsLayer3: false
    }
  },
  methods: {
    getRandom(min, max, notInteger) {
      // notInteger為true 回傳至小數點後2位 以千位數為單位; ex: 400 -> 0.4, 1500 -> 1.5
      if(notInteger) {
        return (Math.floor(Math.random() * max) + min) * 0.001;
      }
      return Math.floor(Math.random() * max) + min;
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      this.showbox = newScroll > this.sectionIndex * this.windowHeight ? true : false;
      const offset = this.sectionIndex * this.windowHeight;
      // 待改 使用data showDots
      this.dotsLayer1 = newScroll > this.sectionIndex * this.windowHeight ? true : false;
      this.dotsLayer2 = newScroll - offset > this.windowHeight * 0.33 ? true : false;
      this.dotsLayer3 = newScroll - offset > this.windowHeight * 0.66 ? true : false;
    },
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
#point svg {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}
#point svg path {
  transition: 1s;
}

@media screen and (max-width: 480px) {
  #point svg {
    opacity: .65;
  }
}
</style>
