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
        <g>
          <polygon fill="#505050" points="156.9,151.3 176.8,76.9 257.1,76.9 261.7,59.7 163.6,59.7 134.4,168.5 204.5,168.5 209.1,151.3 "/>
          <polygon fill="#505050" points="127.1,260.1 131.7,242.9 195.1,242.9 219.6,151.3 237.5,151.3 208.3,260.1" />
        </g>
        <g>
          <polygon fill="#505050" points="293.9,360.4 327.1,236.4 299.6,236.4 304.2,219.2 349.6,219.2 311.8,360.4" />
          <polygon fill="#505050" points="216,318.3 269.7,117.9 341.5,117.9 336.9,135.1 282.9,135.1 238.4,301.1 299.6,301.1 295,318.3 "/>
        </g>
        <g>
          <path fill="#505050" d="M184.2,307c-8.3,0-15.1-6.8-15.1-15.1s6.8-15.1,15.1-15.1c8.3,0,15.1,6.8,15.1,15.1S192.5,307,184.2,307z" />
          <path fill="#505050" d="M105.4,276.8L105.4,276.8c0.1-11.9,2.3-23.3,6.3-33.9H88.5c-3.3,11-5.1,22.7-5.1,34.8h0.1 c0.4,55.5,38.4,102.1,89.9,115.7l5.6-21.2C136.6,361.1,105.4,322.6,105.4,276.8z" />
          <path fill="#505050" d="M149.2,276.8l-21.8-0.1c0.2,35.4,24.4,65.3,57.2,74.1l5.5-21C166.7,323.5,149.3,302.1,149.2,276.8z" />
          <circle fill="#505050" cx="184.2" cy="291.9" r="15.1" />
        </g>
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
