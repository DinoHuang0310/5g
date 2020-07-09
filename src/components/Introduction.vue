<template>
  <div
    v-if="showbox"
    class="introduction"
    :style="{
      'opacity': setOpacity(),
      'transform': setTransform()
    }"
  >
    <slot />
  </div>
</template>

<script>
export default {
  data() {
    return {
      showbox: false,
    }
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
    sectionIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    setOpacity() {
      if(this.scrollTop < 0) {
        return 1;
      }
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        if(this.sectionIndex === 0) {
          const percentage = -1 / this.windowHeight;
          return `${this.scrollTop * percentage + 1}`;
        } else {
          const percentage = 1 / (this.windowHeight * 0.5);
          const offset = this.sectionIndex * this.windowHeight;
          return `${(this.scrollTop - offset) * percentage}`;
        }
      } else {
        // next cut
        if(this.sectionIndex === 0.5) {
          const percentage = -1 / this.windowHeight;
          const myScrollTop = this.scrollTop - this.windowHeight;
          const val = myScrollTop * percentage + 1 < 0 ? 0 : myScrollTop * percentage + 1;
          return val;
        }
        return 0;
      }
    },
    setTransform() {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        if(this.sectionIndex === 0) {
          const percentage = -100 / this.windowHeight;
          return `translate(0, ${this.scrollTop * percentage + -50}%)`;
        }
      } else {
        // next cut
        if(this.sectionIndex === 0.5) {
          const offset = this.sectionIndex * this.windowHeight;
          const percentage = -100 / this.windowHeight;
          const myScrollTop = this.scrollTop - offset;
          const val = myScrollTop * percentage + 50 < -150 ? -150 : myScrollTop * percentage + 50
          return `translate(0, ${val}%)`;
        }
      }
    }
  },
  mounted() {
    if(this.scrollTop >= this.sectionIndex * this.windowHeight) {
      this.showbox = true;
    } else {
      this.showbox = false;
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      if(newScroll >= this.sectionIndex * this.windowHeight) {
        this.showbox = true;
      } else {
        this.showbox = false;
      }
    },
  }
}
</script>

<style>
.introduction {
  position: absolute;
  width: 100%;
  text-align: center;
  color: white;
  opacity: 0;
  top: 50%;
  left: 0;
  transform: translate(0, -50%);
}
.introduction p {
  margin: 1em;
  font-size: 2em;
  font-weight: 400;
  text-shadow: 0 0 15px rgba(0, 0, 0, 1);
}
.introduction p span {
  display: inline-block;
  border: solid 2px white;
  padding: 0.2em 0.5em;
}

@media screen and (max-width: 480px) {
  .introduction p {
    font-size: 1.5em;
    white-space: nowrap;
  }
}
</style>
