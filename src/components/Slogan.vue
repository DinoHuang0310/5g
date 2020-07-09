<template>
  <div
    id="introduction"
    class="area"
    v-if="scrollTop > sectionIndex * windowHeight"
    :style="{'opacity': setOpacity()}"
  >
    <div :style="{'transform': setTransform(), 'opacity': setOpacity(true)}">
      <div class="leftline" />
      <h1><img src="../assets/images/logo.svg" alt="5G投資全攻略 聚焦疫後新錢景" /></h1>
      <div class="rightline" />
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
    }
  },
  methods: {
    setOpacity(isLogo) {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const offset = this.sectionIndex * this.windowHeight;
        const myScrollTop = this.scrollTop - offset;
        const percentage = 1 / this.windowHeight;
        return myScrollTop * percentage > 1 ? 1 : myScrollTop * percentage;
      }
      // next cut
      if(isLogo) {
        const offset = (this.sectionIndex + 1.5) * this.windowHeight;
        if(this.scrollTop > offset) {
          const myScrollTop = this.scrollTop - offset;
          const percentage = -1 / this.windowHeight;
          return myScrollTop * percentage + 1 < 0 ? 0 : myScrollTop * percentage + 1;
        }
      }
    },
    setTransform() {
      const offset = this.sectionIndex * this.windowHeight;
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const percentage = -1 / this.windowHeight;
        return `scale(${(this.scrollTop - offset) * percentage + 2 < 1 ? 1 : (this.scrollTop - offset) * percentage + 2})`;
      }
    }
  }
}
</script>

<style>
#introduction {
  background: black;
  color: white;
}
#introduction > div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}
h1 {
  width: 40%;
  max-width: 700px;
}
h1 img {
  width: 100%;
}
.leftline {
  flex: 1;
  margin-right: 2%;
  height: 1px;
  background-image: linear-gradient(to right, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 1) 100%);
}
.rightline {
  flex: 1;
  margin-left: 2%;
  height: 1px;
  background-image: linear-gradient(to right, rgba(255, 255, 255, 1) 0%, rgba(255, 255, 255, 0) 100%);
}

@media screen and (max-width: 480px) {
  h1 {
    width: 70%;
  }
}
</style>
