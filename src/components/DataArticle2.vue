<template>
  <article
    v-if="showbox"
    id="data-article2"
    class="area"
    :style="{'clip': `rect(${setRect})`}"
  >
    <!-- <h2 :style="{'transform': setTranslate(true)}"> -->
    <h2>
      <span>後疫情時代<br />聚焦5G投資契機</span>
    </h2>
    <div :style="{'transform': setTranslate(false)}">
      <h3><mark>後疫情時代</mark>聚焦5G投資契機</h3>
      <div>
        <p class="first-letter">
          至於5G概念股，表現是否勝過大盤？從以下幾檔美股走勢，可見端倪，包括蘋果(Apple)、亞馬遜(Amazon)、網飛(Netflix)和輝達(Nvidia)，今年以來，累計都有約24%以上的漲幅；同期那斯達克指數僅上漲13.76%，道瓊、標普500指數，則都下跌。
        </p>
        <ul>
          <li>
            <figure>
              <img src="../assets/images/logo-nvidia.png" alt="Nvidia" />
              <figcaption>輝達 Nvidia</figcaption>
            </figure>
            <div class="chart-bar">
              <div :style="{'width': `${setWidth(nvidia)}%`}" />
            </div>
            <span class="number-data">{{ nvidia }}%</span>
          </li>
          <li>
            <figure>
              <img src="../assets/images/logo-apple.png" alt="Apple" />
              <figcaption>蘋果 Apple</figcaption>
            </figure>
            <div class="chart-bar">
              <div :style="{'width': `${setWidth(apple)}%`}" />
            </div>
            <span class="number-data">{{ apple }}%</span>
          </li>
          <li>
            <figure>
              <img src="../assets/images/logo-amazon.png" alt="Amazon" />
              <figcaption>亞馬遜 Amazon</figcaption>
            </figure>
            <div class="chart-bar">
              <div :style="{'width': `${setWidth(amazon)}%`}" />
            </div>
            <span class="number-data">{{ amazon }}%</span>
          </li>
          <li>
            <div>
              <figure>
                <img src="../assets/images/logo-netflix.png" alt="Netflix" />
                <figcaption>網飛 Netflix</figcaption>
              </figure>
            </div>
            <div class="chart-bar">
              <div :style="{'width': `${setWidth(netflix)}%`}" />
            </div>
            <span class="number-data">{{ netflix }}%</span>
          </li>
        </ul>
        <div class="chart-title">
          <span>股價漲幅</span>
          <small>資料來源：CNBC (統計至7月2日收盤)</small>
        </div>
      </div>
    </div>
  </article>
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
      nvidia: 0,
      apple: 0,
      amazon: 0,
      netflix: 0
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      if(newScroll > this.sectionIndex * this.windowHeight) {
        this.showbox = true;
        this.nvidia = this.setVal(63.40);
        this.apple = this.setVal(23.99);
        this.amazon = this.setVal(56.42);
        this.netflix = this.setVal(47.38);
      } else {
        this.showbox = false;
      }
    },
  },
  computed: {
    setRect() {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const offset = this.sectionIndex * this.windowHeight;
        return `${this.windowHeight - (this.scrollTop - offset)}px ${this.windowWidth}px ${this.windowHeight}px 0px`;
      }
      return `0px ${this.windowWidth}px ${this.windowHeight}px 0px`;
    }
  },
  methods: {
    setTranslate(staytop) {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = (100 / this.windowHeight) * -1;
      if(staytop) {
        const val = (this.scrollTop - offset) * percentage + 100 > 0 ? (this.scrollTop - offset) * percentage + 100 : 0;
        return `translate(0, ${val}%)`;
      }
      return `translate(0, ${(this.scrollTop - offset) * percentage + 100}%)`;
    },
    setVal(max) {
      const offset = this.sectionIndex * this.windowHeight;
      const myScrollTop = this.scrollTop - offset;
      const percentage = max / (this.windowHeight * 0.8);
      const val = myScrollTop * percentage < max ? myScrollTop * percentage : max;
      return val.toFixed(2);
    },
    setWidth(num) {
      return num / 63.40 * 100; // 4間數值最大的為100%
    }
  }
}
</script>

<style>
#data-article2 h2:before {
  background-image: url("../assets/images/data-article2.png");
}
#data-article2 ul {
  padding: 0.5em 0;
}
#data-article2 li {
  display: flex;
  align-items: center;
  margin: 1em 0;
}
#data-article2 figure {
  display: flex;
  align-items: center;
  width: calc(9vw + 40px);
  min-width: 150px;
}
#data-article2 figcaption {
  margin: 0 0.5em;
}
.chart-bar {
  position: relative;
  flex: 1;
  height: 1px;
  background-image: url("../assets/images/dashed.jpg");
  background-repeat: repeat-x;
}
.chart-bar div {
  position: absolute;
  height: 5px;
  background: #505050;
  left: 0;
  top: -2px;
}
#data-article2 .number-data {
  font-size: 2vw;
  width: 8vw;
  text-align: right;
}

@media (orientation: portrait) {
  #data-article2 h2:before {
    opacity: .6;
  }
}

@media screen and (min-width: 768px) and (max-width: 1024px) and (orientation: portrait) {
  #data-article1 .number-data {
    font-size: 7vw;
  }
  #data-article2 figure {
    width: calc(16vw + 40px);
  }
  #data-article2 .number-data {
    font-size: 3vw;
    width: 4em;
  }
}

@media screen and (max-width: 1366px) {
  #data-article2 figure {
    width: calc(16vw + 40px);
  }
}

@media screen and (max-width: 768px) {
  #data-article2 figure img {
    width: 20px;
  }
}

@media screen and (max-width: 480px) {
  #data-article2 ul {
    padding: 0;
  }
  #data-article2 li {
    justify-content: space-between;
    margin: 0.5em 0;
  }
  #data-article2 figcaption {
    margin-right: 0;
  }
  .chart-bar {
    margin: 0 0.8em;
  }
  .chart-bar div {
    display: none;
  }
  #data-article2 .number-data {
    width: auto;
    font-size: 6vw;
  }
  #data-article2 figure {
    min-width: auto;
    width: auto;
  }
}
</style>
