<template>
  <div
    v-if="showbox"
    class="area transitions"
    :style="{'opacity': setOpacity()}"
  >
    <svg
      version="1.1"
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      viewBox="0 0 450 450"
      :style="{'transform': setTransform()}"
    >
      <g>
        <circle
          cx="50%"
          cy="50%"
          r="210px"
          fill="#ffffff"
          stroke="#505050"
          stroke-width="20"
          stroke-dasharray="1319"
          :stroke-dashoffset="setLineAnimate({
            'type': 'draw',
            'direction': -1,
            'range': 420 * Math.PI,
          })"
        />
      </g>
      <g>
        <path fill="#505050" d="M349.5,203.2L349.5,203.2L349.5,203.2h-59.5c-18.7,0-35.1,7.9-49,23.4c-5.6,6.4-10.3,13.3-14.1,20.6
          c-1.6-5.8-3.6-11.1-6.4-16.5c-6.2-11.7-14.5-21-24.8-27.4c-10.3-6.5-21.2-9.7-32.7-9.7c-3.2,0-7.3,0.2-12.7,0.8l16.7-56.8h75.8
          l6.9-23.2h-99.4L117.9,223c13.3-5.4,25.8-8.1,37.3-8.1c14.7,0,27,5.2,36.5,15.3c9.5,10.3,14.3,23.6,14.3,39.9
          c0,19.3-6,34.7-17.7,46c-11.7,11.3-24.8,17.1-39.1,17.1c-10.7,0-20.6-3.2-29.6-9.5c-9.1-6.4-16.3-15.9-21.8-28.6L76,304.6
          c8.1,17.7,18.3,30.8,30.4,38.9c12.1,8.3,26.2,12.5,42.1,12.5c15.1,0,28.6-3.6,40.7-10.7c11.3-6.7,20.6-16.5,28-29
          c1,3.6,2.2,7.1,3.8,10.5c7.1,15.5,19.3,23.2,35.7,23.2h62.1h3.6l0.8-3.4l11.7-52c2.8-12.3,1.8-21-3-26.2l0,0l0,0
          c-3.6-3.8-9.5-5.6-18.1-5.6h-34.5h-4l-0.4,3.8l-1.8,16.1l-0.6,5h5h25.4c5.2,0,7.1,0.6,7.5,0.8c0.2,0.6,0.6,2.6-0.6,7.9l-6.5,29.4
          h-41.9c-9.5,0-15.5-4-18.9-12.7l0,0l0,0c-3.4-8.5-3.6-20-0.8-34.3c3-14.5,8.1-26.4,15.5-35.3c8.1-10.1,17.5-14.9,28.6-14.9h58.7
          h3.2l1-3.2l5-16.3l1.8-5.6h-6V203.2z" />
        <path fill="#505050" d="M283,85.5l-4.4,15.1c49.4,6.2,81.4,40.5,77,82.8h18.5C377.7,134.1,340.5,94.2,283,85.5z M264.1,152.8
          l-8.5,30.6h37.1C296.1,167.1,283.8,153.8,264.1,152.8z M274.3,116.9l-5,17.3c30.8,2.2,50.4,23.2,45.8,49.2h21
          C340.9,149,314.9,121,274.3,116.9z" />
      </g>
    </svg>
  </div>
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
    sectionIndex: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      showbox: false
    }
  },
  methods: {
    setOpacity() {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const offset = this.sectionIndex * this.windowHeight;
        const percentage = 1 / this.windowHeight;
        const myScrollTop = this.scrollTop - offset;
        return myScrollTop * percentage > 1 ? 1 : myScrollTop * percentage;
      }
      // next cut
    },
    setTransform() {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const offset = this.sectionIndex * this.windowHeight;
        const percentage = -5 / this.windowHeight;
        return `scale(${(this.scrollTop - offset) * percentage + 5 < 1 ? 1 : (this.scrollTop - offset) * percentage + 5})`;
      }
      // next cut
    },
    setLineAnimate(setting) {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = setting.range / this.windowHeight * setting.direction;
      const myScrollTop = this.scrollTop - offset;
      switch(setting.type) {
        case 'dash':
          return myScrollTop * percentage;
        case 'draw':
          return myScrollTop * percentage + setting.range < 0 ? 0 : myScrollTop * percentage + setting.range;
      }
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      this.showbox = newScroll > this.sectionIndex * this.windowHeight ? true : false;
    },
  },
}
</script>

<style>
.transitions {
  background: white;
  display: flex;
  justify-content: center;
  align-items: center;
  pointer-events: none;
}
.transitions svg {
  width: 80%;
  max-width: 450px;
}

@media screen and (max-width: 1366px) {
  .transitions svg {
    width: 40%;
  }
}

@media screen and (max-width: 480px) {
  .transitions svg {
    width: 60%;
  }
}
</style>
