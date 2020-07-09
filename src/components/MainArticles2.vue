<template>
  <div
    v-show="showbox"
    class="area"
    id="main-articles2"
    :style="{'opacity': setOpacity()}"
  >
    <figure :style="{'transform': setTranslate(10)}">
      <img src="../assets/images/mainarticle3.png" alt="台灣5G新創連國際都驚豔！用臉量心跳  虛擬人物帶你走" />
      <figcaption><img src="../assets/images/article2-1.png" alt="台灣5G新創連國際都驚豔！用臉量心跳  虛擬人物帶你走" /></figcaption>
      <a class="readmore" href="https://www.businesstoday.com.tw/article/category/80393/post/202006220009/%E7%94%A8%E8%87%89%E9%87%8F%E5%BF%83%E8%B7%B3%E3%80%81%E8%BF%B7%E8%B7%AF%E6%9C%89%E8%99%9B%E6%93%AC%E4%BA%BA%E7%89%A9%E5%B8%B6%E4%BD%A0%E8%B5%B0%E3%80%80%E5%8F%B0%E7%81%A35G%20%E6%96%B0%E5%89%B5%E6%87%89%E7%94%A8%EF%BC%8C%E7%82%BA%E4%BD%95%E9%80%A3%E5%A4%96%E5%9C%8B%E5%B8%82%E5%A0%B4%E9%83%BD%E9%A9%9A%E8%B1%94%EF%BC%9F" target="_blank">
        <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
          <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
        </svg>
        more
      </a>
    </figure>
    <figure :style="{'transform': setTranslate(-10)}">
      <img src="../assets/images/mainarticle2.png" alt="5G不只網速快 還有三大特點《一級玩家》科幻場景逐步實現！" />
      <figcaption><img src="../assets/images/article2-2.png" alt="5G不只網速快 還有三大特點《一級玩家》科幻場景逐步實現！" /></figcaption>
      <a class="readmore" href="https://www.businesstoday.com.tw/article/category/80393/post/202006200005/%E9%99%A4%E4%BA%86%E7%B6%B2%E9%80%9F%E8%AE%8A%E5%BF%AB%E9%82%84%E8%83%BD%E5%B9%B9%E5%98%9B%EF%BC%9F5G%E3%80%8C%E4%B8%89%E5%A4%A7%E7%89%B9%E9%BB%9E%E3%80%8D%E5%8F%AF%E6%9C%9B%E4%BD%BF%E3%80%8A%E4%B8%80%E7%B4%9A%E7%8E%A9%E5%AE%B6%E3%80%8B%E7%A7%91%E5%B9%BB%E5%A0%B4%E6%99%AF%E9%80%90%E6%AD%A5%E5%AF%A6%E7%8F%BE%EF%BC%81" target="_blank">
        <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
          <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
        </svg>
        more
      </a>
    </figure>
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
  methods: {
    setOpacity() {
      if(this.scrollTop > (this.sectionIndex * this.windowHeight)) {
        const offset = this.sectionIndex * this.windowHeight;
        const percentage = 1 / (this.windowHeight * 0.6);
        return (this.scrollTop - offset) * percentage > 1 ? 1 : (this.scrollTop - offset) * percentage;
      }
    },
    setTranslate(direction) {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = direction / (this.windowHeight * 0.6);
      const myScrollTop = this.scrollTop - offset;
      let val;
      if(direction < 0) {
        val = myScrollTop * percentage < direction ? direction : myScrollTop * percentage;
      } else {
        val = myScrollTop * percentage > direction ? direction : myScrollTop * percentage;
      }
      return this.windowWidth > this.windowHeight ? `translate(${val / 4 * -1}%, ${val}%)` : `translate(0, ${val * -1}%)`;

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
#main-articles2 {
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f6f6f6;
  padding: 5%;
}
#main-articles2 figure {
  width: 43%;
  max-width: 760px;
  transform: translate(0, 0);
}
#main-articles2 figure img {
  display: block;
}
#main-articles2 figcaption {
  padding: 0.5em 5% 0;
  font-weight: 300;
}
#main-articles2 figcaption img {
  width: 68%;
}

@media (orientation: portrait) {
  #main-articles2 {
    flex-wrap: wrap;
    align-content: center;
  }
  #main-articles2 figure {
    text-align: right;
  }
  #main-articles2 figcaption {
    text-align: left;
    font-weight: 400;
    padding: 0.4em 4%;
  }
  #main-articles2 figcaption img {
    width: 90%;
  }
  #main-articles2 a.readmore {
    position: relative;
    display: inline-block;
    bottom: 0;
  }
}

@media screen and (max-width: 1024px) and (orientation: portrait) {
  #main-articles2 figure {
    width: 60%;
  }
}

@media screen and (max-width: 768px) and (orientation: portrait) {
  #main-articles2 figure {
    width: 70%;
  }
}

@media screen and (max-width: 480px) and (orientation: portrait) {
  #main-articles2 figure {
    width: 100%;
  }
}
</style>
