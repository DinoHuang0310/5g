<template>
  <footer
    v-if="showbox"
    class="area"
    :style="setRect"
  >
    <div :style="{'transform': desktopTranslate(true)}">
      <div style="max-width: 90%">
        <div style="display: inline-block; text-align: left;">
          <dl>
            <dt><span>內容監製</span>今周刊</dt>
            <dt><span>專題製作</span>今周刊 數位內容部</dt>
          </dl>
        </div>
        <p>
          數位Copyright &#169; {{ year }} 今周刊.All rights reserved.<br />
          版權所有，禁止擅自轉貼節錄
        </p>
      </div>
    </div>
  </footer>
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
      year: new Date().getFullYear(),
    }
  },
  watch: {
    scrollTop: function(newScroll) {
      this.showbox = newScroll > this.sectionIndex * this.windowHeight ? true : false;
    },
  },
  computed: {
    setRect() {
      if(this.scrollTop < (this.sectionIndex + 1) * this.windowHeight) {
        const offset = this.sectionIndex * this.windowHeight;
        return `clip: rect(${this.windowHeight - (this.scrollTop - offset)}px ${this.windowWidth}px ${this.windowHeight}px 0px)`;
      }
      return `clip: rect(0px ${this.windowWidth}px ${this.windowHeight}px 0px)`;
    },
  },
  methods: {
    desktopTranslate(staytop) {
      const offset = this.sectionIndex * this.windowHeight;
      const percentage = -100 / this.windowHeight;
      if(staytop) {
        const val = (this.scrollTop - offset) * percentage + 100 > 0 ? (this.scrollTop - offset) * percentage + 100 : 0;
        return `translate(0, ${val}%)`;
      }
      return `translate(0, ${(this.scrollTop - offset) * percentage + 100}%)`;
    }
  }
}
</script>

<style>
footer {
  background: #f6f6f6;
  text-align: center;
}
footer, footer p {
  font-size: 0.8em;
  letter-spacing: 3px;
}
footer p {
  line-height: 2;
}
footer > div {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
footer dt {
  margin: 0.8em 0;
}
footer dt span {
  display: inline-block;
  background: #505050;
  color: white;
  padding: 0.1em 0.85em;
  padding-right: calc(0.8em - 3px);
  border-radius: 1em;
  margin-right: 1em;
}
@media screen and (max-width: 480px) {
  footer, footer p {
    font-size: 1em;
    letter-spacing: initial;
  }
  footer br {
    display: none;
  }
  footer dt span {
    padding-right: 0.85em;
  }
}
</style>
