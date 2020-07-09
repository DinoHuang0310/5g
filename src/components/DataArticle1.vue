<template>
  <article
    v-if="showbox"
    id="data-article1"
    class="area"
    :style="{'clip': `rect(${setRect})`}"
  >
    <!-- <h2 :style="{'transform': setTranslate(windowWidth > 480 ? true : false)}"> -->
    <h2>
      <span>Q1全球5G手機出貨量年增逾28%</span>
    </h2>
    <div :style="{'transform': setTranslate(false)}">
      <h3>Q1全球5G手機出貨量年增逾28%</h3>
      <div>
        <p class="first-letter">
          市場研究機構 Strategy Analytics 報告顯示，<br>
          2020年首季，全球5G手機出貨量，達2410萬支，高於2019年同期的1870萬支，顯示在疫情影響下，5G手機需求依然強勁。
        </p>
        <ul>
          <li>
            <span class="data-title">2019 Q1</span>
            <span class="number-data">18,700,000<span>支</span></span>
          </li>
          <li>
            <span class="data-title">2020 Q1</span>
            <span class="number-data">{{ numberFormat(q12020, 0, '.', ',') }}<span>支</span></span>
          </li>
        </ul>
        <div class="chart-title">
          <span>全球5G手機出貨量</span>
          <small>資料來源：Strategy Analytics</small>
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
      q12020: 0,
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      this.showbox = newScroll > this.sectionIndex * this.windowHeight ? true : false;
      const offset = this.sectionIndex * this.windowHeight;
      // 2020數據
      const data2020 = 24100000 / (this.windowHeight * 0.8);
      const numVal2 = (newScroll - offset) * data2020 < 24100000 ? (newScroll - offset) * data2020 : 24100000;
      this.q12020 = Math.round(numVal2);
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
    numberFormat(n, c, d, t) {
      c = isNaN(c = Math.abs(c)) ? 2 : c;
      d = d == undefined ? "." : d;
      t = t == undefined ? "," : t;
      const s = n < 0 ? "-" : "";
      const i = String(parseInt(n = Math.abs(Number(n) || 0).toFixed(c)));
      let j = (j = i.length) > 3 ? j % 3 : 0;
      return s + (j ? i.substr(0, j) + t : "") + i.substr(j).replace(/(\d{3})(?=\d)/g, "$1" + t) + (c ? d + Math.abs(n - i).toFixed(c).slice(2) : "");
    }
  }
}
</script>

<style>
#data-article1 h2:before {
  background-image: url("../assets/images/data-article1.png");
}
#data-article1 li {
  position: relative;
  text-align: center;
  border-bottom: solid 1px #505050;
  margin: 2em 0;
}
#data-article1 .number-data {
    font-size: 4vw;
    min-width: 10vw;
}
#data-article1 .number-data span {
  font-family: 'Noto Sans TC', sans-serif, 'Microsoft JhengHei', arial;
  font-size: 1vw;
  font-weight: initial;
  margin-left: 0.5em;
}
.data-title {
  position: absolute;
  left: 0;
  bottom: 0.5em;
}

@media (max-width: 480px) {
  #data-article1 li {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin: 1.3em 0;
  }
  .data-title {
    position: relative;
    bottom: auto;
  }
  #data-article1 .number-data {
    font-size: 11vw;
  }
  #data-article1 br {
    display: none;
  }
}
</style>
