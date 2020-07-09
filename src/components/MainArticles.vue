<template>
  <div
    v-show="showbox"
    class="area"
    id="main-articles"
    :style="{'opacity': setOpacity()}"
  >
  <!-- <div
    v-if="showbox"
    class="area"
    id="main-articles"
    :style="{'clip': `rect(${setRect})`, 'transform': setTranslate(false)}"
  > -->
    <!-- <span
      id="borderline"
      :style="{'top': setTop() + '%'}"
    /> -->
    <span id="borderline" />
    <div>
      <div class="article-card">
        <div class="center-card">
          <img src="../assets/images/article-card1.png" alt="5G投資下半年啥最熱門? 這檔龍頭股3個月飆升110%! 手機供應鏈動起來了" />
          <a class="readmore" href="https://www.businesstoday.com.tw/article/category/80402/post/202006220041/5G%E6%8A%95%E8%B3%87%E4%B8%8B%E5%8D%8A%E5%B9%B4%E5%95%A5%E6%9C%80%E7%86%B1%E9%96%80%EF%BC%9F%20%E9%80%99%E6%AA%94%E9%BE%8D%E9%A0%AD%E8%82%A13%E5%80%8B%E6%9C%88%E9%A3%86%E5%8D%87110%EF%BC%85%EF%BC%81%20%E6%89%8B%E6%A9%9F%E4%BE%9B%E6%87%89%E9%8F%88%E5%8B%95%E8%B5%B7%E4%BE%86%E4%BA%86" target="_blank">
            <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
              <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
            </svg>
            more
          </a>
        </div>
      </div>
    </div>
    <div class="rightbox">
      <div>
        <div class="article-card">
          <div class="right-card">
            <img src="../assets/images/article-card2.png" alt="想投資5G基金、ETF? 3張表讓你秒懂4檔商品差異、怎麼買最適合自己" />
            <a class="readmore" href="https://www.businesstoday.com.tw/article/category/80401/post/202006190034/%E6%83%B3%E6%8A%95%E8%B3%875G%E5%9F%BA%E9%87%91%E3%80%81ETF%EF%BC%9F3%E5%BC%B5%E8%A1%A8%E8%AE%93%E4%BD%A0%E7%A7%92%E6%87%824%E6%AA%94%E5%95%86%E5%93%81%E5%B7%AE%E5%9C%A8%E5%93%AA%E3%80%81%E6%80%8E%E9%BA%BC%E8%B2%B7%E6%9C%80%E9%81%A9%E5%90%88%E8%87%AA%E5%B7%B1" target="_blank">
              <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
                <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
              </svg>
              more
            </a>
          </div>
        </div>
      </div>
      <div>
        <div class="article-card">
          <div>
            <img src="../assets/images/article-card3.png" alt="5G基地台供應鏈放量 股價波段強彈30~110%! 還有這支國家隊要注意" />
            <a class="readmore" href="https://www.businesstoday.com.tw/article/category/80402/post/202006240044/5G%E5%9F%BA%E5%9C%B0%E5%8F%B0%E4%BE%9B%E6%87%89%E9%8F%88%E6%94%BE%E9%87%8F%E3%80%80%E8%82%A1%E5%83%B9%E6%B3%A2%E6%AE%B5%E5%BC%B7%E5%BD%8830%EF%BD%9E110%EF%BC%85%EF%BC%81%20%E9%82%84%E6%9C%89%E9%80%99%E6%94%AF%E5%9C%8B%E5%AE%B6%E9%9A%8A%E8%A6%81%E6%B3%A8%E6%84%8F" target="_blank">
              <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
                <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
              </svg>
              more
            </a>
          </div>
        </div>
      </div>
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
    windowWidth: {
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
  computed: {
    setRect() {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const offset = this.sectionIndex * this.windowHeight;
        return `${this.windowHeight - (this.scrollTop - offset)}px ${this.windowWidth}px ${this.windowHeight}px 0px`;
      }
      return `0px ${this.windowWidth}px ${this.windowHeight}px 0px`;
    },
  },
  methods: {
    setOpacity() {
      if(this.scrollTop > (this.sectionIndex * this.windowHeight)) {
        const offset = this.sectionIndex * this.windowHeight;
        const percentage = 1 / (this.windowHeight * 0.5);
        return (this.scrollTop - offset) * percentage > 1 ? 1 : (this.scrollTop - offset) * percentage;
      }
    },
    setTop() {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = -77 / this.windowHeight;
      return (this.scrollTop - offset) * percentage + 100 < 23 ? 23 : (this.scrollTop - offset) * percentage + 100;
    },
    setTranslate(staytop) {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = (100 / this.windowHeight) * -1;
      if(staytop) {
        const val = (this.scrollTop - offset) * percentage + 100 > 0 ? (this.scrollTop - offset) * percentage + 100 : 0;
        return `translate(0, ${val}%)`;
      }
      return `translate(0, ${(this.scrollTop - offset) * percentage + 100}%)`;
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
#main-articles {
  display: flex;
  background: black;
  padding: 5%;
  justify-content: space-between;
}
#borderline {
  position: absolute;
  width: 200%;
  left: 50%;
  top: 23%;
  height: 18%;
  transform: translate(-50%, 0) rotate(15deg);
  border-top: solid 0.6em rgba(80, 80, 80, .05);
  border-bottom: solid 0.6em rgba(80, 80, 80, .05);
}
#main-articles > div {
  width: 47.2222%;
}
.article-card {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  padding: 4%;
  background: #f6f6f6;
}
.article-card > div {
  position: relative;
  display: flex;
  height: 100%;
  align-items: center;
}
.article-card img {
  width: 90%;
  max-width: 630px;
}
.center-card {
  justify-content: center;
}
.right-card {
  justify-content: flex-end;
}
.rightbox {
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
}
.rightbox > div {
  width: 100%;
  height: 50%;
  padding-top: 5.88%;
}
.rightbox > div:first-child {
  padding-top: 0;
  padding-bottom: 5.88%;
}

/* @media screen and (max-width: 480px) { */
@media (orientation: portrait) {
  #main-articles {
    overflow: hidden;
  }
  #main-articles > div {
    position: absolute;
    height: 100%;
    width: 100%;
    padding: 5%;
    left: 0;
    top: 0;
  }
  #main-articles > div.rightbox {
    position: relative;
    padding: 0;
    transform: translate(0, 34%);
  }
  .rightbox > div {
    position: absolute;
    width: 100%;
    height: 32%;
    top: 34%;
    padding-top: 0;
  }
  .rightbox > div:first-child {
    padding-bottom: 0;
    top: 0;
  }
  .article-card {
    height: 32%;
  }
  .article-card img {
    width: 100%;
  }
  .rightbox .article-card {
    height: 100%;
  }
}
</style>
