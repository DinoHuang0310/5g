<template>
  <div
    v-if="showbox"
    class="area fadein-model"
    :style="{'opacity': setOpacity()}"
  >
    <div
      :style="{'transform': setTransform(outAnimate)}"
    >
      <div v-if="showLine" class="leftline" />
      <div class="modelcontent">
        <slot />
      </div>
      <div v-if="showLine" class="rightline" />
    </div>
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
    },
    showLine: {
      type: Boolean,
      default: false
    },
    outAnimate: {
      type: String,
      default: 'scale'
    }
  },
  data() {
    return {
      showbox: false
    }
  },
  methods: {
    setOpacity() {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = 1 / (this.windowHeight * 0.7);
      return (this.scrollTop - offset) * percentage > 1 ? 1 : (this.scrollTop - offset) * percentage;
    },
    setTransform(type) {
      if(this.scrollTop > (this.sectionIndex + 1) * this.windowHeight) {
        const offset = (this.sectionIndex + 1) * this.windowHeight;
        const myScrollTop = this.scrollTop - offset;
        if(type === 'scale') {
          // 放大出場
          const percentage = 3 / this.windowHeight;
          return `scale(${myScrollTop * percentage + 1 > 3 ? 3 : myScrollTop * percentage + 1})`;
        } else if(type === 'translate') {
          // 滾動出場
          const percentage = -100 / this.windowHeight;
          return `translate(0, ${myScrollTop * percentage}%)`;
        }
      } else {
        return type === 'scale' ? 'scale(1)' : 'translate(0, 0)';
      }
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      this.showbox = newScroll > this.sectionIndex * this.windowHeight ? true : false;
    }
  }
}
</script>

<style>
.fadein-model {
  /* color: white; */
  background: #f6f6f6;
  pointer-events: none;
}
.fadein-model > div {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  height: 100%;
}
.fadein-model div {
  position: relative;
}
.fadein-model p {
  line-height: 2;
  width: 80%;
  margin: 1em auto;
}
.fadein-model a.readmore {
  position: relative;
  display: inline-block;
}
.modelcontent {
  pointer-events: auto;
}

@media screen and (min-width: 768px) and (max-width: 1024px) and (orientation: portrait) {
  .fadein-model p {
    letter-spacing: 4px;
  }
}

@media screen and (max-width: 480px) {
  .fadein-model p {
    width: 90%;
    letter-spacing: initial;
  }
}
</style>
