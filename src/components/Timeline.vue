<template>
  <div
    id="timeline"
    v-if="showbox"
    class="area"
    :style="{'opacity': setOpacity()}"
  >
    <div>
      <article>
        <h2>5G企業專網需求超出預期<br /> 測試家數估逾<span class="number-data">{{ num }}</span>家</h2>
        <p>勤業眾信聯合會計師事務所《2020全球高科技、媒體及電信產業趨勢》報告原預期，2020年，全球會有100家以上的大型企業，開始測試5G企業專網；值得注意的是，在疫情影響下，2020年首季，實際進行測試的企業數，已超過預期，2020全年，預計將上修至超過1000家。</p>
      </article>
      <div id="bar" :style="{'width': barWidth + '%'}" />
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
  data() {
    return {
      showbox: false,
      barWidth: 0,
      num: 0
    }
  },
  methods: {
    setOpacity() {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = 1 / (this.windowHeight * 0.7);
      return (this.scrollTop - offset) * percentage > 1 ? 1 : (this.scrollTop - offset) * percentage;
    },
  },
  watch: {
    scrollTop: function(newScroll) {
      if(newScroll > this.sectionIndex * this.windowHeight) {
        this.showbox = true;
        const offset = this.sectionIndex * this.windowHeight;
        const percentage = 100 / (this.windowHeight * 0.7);
        const barWidthVal = (newScroll - offset) * percentage < 100 ? (newScroll - offset) * percentage : 100;
        this.barWidth = barWidthVal;
        const percentage2 = 1000 / (this.windowHeight * 0.7);
        const numVal = (newScroll - offset) * percentage2 < 1000 ? (newScroll - offset) * percentage2 : 1000;
        this.num = Math.round(numVal);
      } else {
        this.showbox = false;
        this.barWidth = 0;
        this.num = 0;
      }
    },
  }
}
</script>

<style>
#timeline > div {
  color: white;
  height: 100%;
  padding: 5%;
}
#timeline article {
  text-align: center;
  height: 100%;
}
#timeline article h2 {
  font-weight: 400;
  letter-spacing: 4px;
  margin: 0;
  padding-bottom: 0.5em;
  height: 50%;
  display: flex;
  justify-content: center;
  align-items: flex-end;
}
#timeline h2 br {
  display: none;
}
#timeline .number-data {
  display: inline-block;
  font-size: 1.5em;
  min-width: 2.6em;
}
#timeline article p {
  line-height: 2;
  width: 80%;
  margin: 1em auto;
}
#bar {
  position: fixed;
  top: 50%;
  left: 0;
  height: 1px;
  background: linear-gradient(to right, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 1) 100%);
}

@media (orientation: portrait) {
  #timeline article p {
    width: 100%;
    line-height: initial;
  }
  #timeline > div {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #timeline article {
    height: auto;
  }
  #timeline article h2 {
    display: block;
    height: auto;
  }
  #timeline h2 br {
    display: block;
  }
  #bar {
    display: none;
  }
}

@media screen and (max-width: 480px) {
  #timeline .number-data {
    font-size: 11vw;
  }
}
</style>
