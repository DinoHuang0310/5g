<template>
  <div
    id="app"
    :style="{'height': windowHeight * 16 + 'px'}"
    v-if="windowHeight"
  >
    <header>
      <div id="btnet-logo">
        <a href="https://www.businesstoday.com.tw" target="_black">
          <img src="./assets/images/businesstoday.svg" alt="今周刊" />
        </a>
      </div>
      <div class="socialmedias">
        <a href="http://www.facebook.com/share.php?u=https://www.businesstoday.com.tw/topic/2020/5g" target="_blank"><span class="icon-facebook2" /></a>
        <a href="https://social-plugins.line.me/lineit/share?url=https://www.businesstoday.com.tw/topic/2020/5g" target="_blank"><span class="icon-line" /></a>
      </div>
    </header>
    <AnimateBox
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
    />
    <Slogan
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="2"
    />
    <Point
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :windowWidth="windowWidth"
      :sectionIndex="4.5"
    />
    <Timeline
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="4.5"
    />
    <DataArticle1
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :windowWidth="windowWidth"
      :sectionIndex="5.5"
    />
    <DataArticle2
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :windowWidth="windowWidth"
      :sectionIndex="6.5"
    />
    <Transitions
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="8"
    />
    <FadeInModel
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="9"
    >
      <h2>投資標的 怎麼選?</h2>
    </FadeInModel>
    <MainArticles
      :scrollTop="scrollTop"
      :windowWidth="windowWidth"
      :windowHeight="windowHeight"
      :sectionIndex="10"
    />
    <!-- <Transitions
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="11"
    /> -->
    <FadeInModel
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="11"
    >
      <h2 style="text-align: center">5G商機在哪裡？</h2>
    </FadeInModel>
    <MainArticles2
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :windowWidth="windowWidth"
      :sectionIndex="12"
    />
    <FadeInModel
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :sectionIndex="13"
      outAnimate="translate"
    >
      <p class="first-letter">
        5G所引爆的，不只是一場產業革命，其中隱含的投資機會，更是市場高度關注的焦點，唯有掌握趨勢、超前部署，才能精準掌握後疫情時代的財富重分配契機。
      </p>
      <div class="readbox">
        <a href="https://www.businesstoday.com.tw/article/category/80393/post/202006200013/4%E5%AE%B6%E5%A4%A7%E5%92%96%E5%85%AC%E5%8F%B8%E8%82%A1%E5%83%B9%E6%BC%B2%E5%B9%85%E5%8B%9D%E5%A4%A7%E7%9B%A4%EF%BC%81%E4%B8%80%E6%96%87%E6%8E%8C%E6%8F%A1%E3%80%8C3%E7%B5%84%E9%97%9C%E9%8D%B5%E6%95%B8%E6%93%9A%E3%80%8D%E3%80%80%E8%81%9A%E7%84%A6%E5%BE%8C%E7%96%AB%E6%83%85%E6%99%82%E4%BB%A35G%E6%8A%95%E8%B3%87%E8%B6%A8%E5%8B%A2" class="readmore" target="_blank">
          <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
            <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
          </svg>
          more
        </a>
      </div>
    </FadeInModel>
    <Footer
      :scrollTop="scrollTop"
      :windowHeight="windowHeight"
      :windowWidth="windowWidth"
      :sectionIndex="14"
    />
    <transition>
      <button id="backtop" v-show="showButton" @click="backTop(1000)">
        Go Top
        <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 100 20">
          <polygon points="85.9,5.1 85.2,5.8 98.4,19 0,19 0,20 100,20 100,19.2" fill="#505050" />
        </svg>
      </button>
    </transition>
  </div>
</template>

<script>
import AnimateBox from './components/AnimateBox.vue'
import Slogan from './components/Slogan.vue'
import Point from './components/Point.vue'
import Timeline from './components/Timeline.vue'
import DataArticle1 from './components/DataArticle1.vue'
import DataArticle2 from './components/DataArticle2.vue'
import Transitions from './components/Transitions.vue'
import FadeInModel from './components/FadeInModel.vue'
import MainArticles from './components/MainArticles.vue'
import MainArticles2 from './components/MainArticles2.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    AnimateBox,
    Slogan,
    Point,
    Timeline,
    DataArticle1,
    DataArticle2,
    Transitions,
    FadeInModel,
    MainArticles,
    MainArticles2,
    Footer
  },
  data() {
    return {
      scrollTop: 0,
      windowHeight: null,
      windowWidth: null,
      showButton: false
    }
  },
  methods: {
    // setScrollTop() {
    //   this.scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
    // },
    checkScreen() {
      const clientWidth = document.documentElement.clientWidth;
      if(clientWidth !== this.windowWidth) {
        const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
        this.windowWidth = clientWidth;
        this.windowHeight = isMobile ? screen.height : document.documentElement.clientHeight;
      }
    },
    backTop(duration) {
      if (document.scrollingElement.scrollTop === 0) return;
      const totalScrollDistance = document.scrollingElement.scrollTop;
      let scrollY = totalScrollDistance, oldTimestamp = null;
      function step (newTimestamp) {
        if (oldTimestamp !== null) {
          scrollY -= totalScrollDistance * (newTimestamp - oldTimestamp) / duration;
          if (scrollY <= 0) return document.scrollingElement.scrollTop = 0;
          document.scrollingElement.scrollTop = scrollY;
        }
        oldTimestamp = newTimestamp;
        window.requestAnimationFrame(step);
      }
      window.requestAnimationFrame(step);
    },
    handleScroll() {
      this.scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
      if (window.scrollY > (window.innerHeight * 2)) {
        this.showButton = true;
      } else {
        this.showButton = false;
      }
    },
  },
  // created () {
  //   window.addEventListener('scroll', this.handleScroll);
  // },
  mounted() {
    window.addEventListener('scroll', this.handleScroll, false);
    window.addEventListener('resize', this.checkScreen);
    this.checkScreen();
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
    window.removeEventListener('resize', this.checkScreen);
  },
  // destroyed () {
  //   if(this.goTop) window.removeEventListener('scroll', this.handleScroll);
  // }
}
</script>

<style src='./assets/css/style.css'></style>
<style src='./assets/icons/style.css'></style>
<style>
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 0.5em;
  z-index: 1;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
header span {
  font-size: 30px;
  display: inline-block;
  padding: 0.3em;
}
.readbox {
  position: absolute;
  width: 100%;
  bottom: -3vw;
}
#btnet-logo img {
  display: inline-block;
  width: 100px;
}
#backtop {
  position: fixed;
  font-size: 20px;
  font-family: 'Montserrat', sans-serif;
  font-style: italic;
  color: #505050;
  right: 0;
  bottom: calc(50px + 1em);
  display: block;
  padding: 0;
  padding-right: 2.4em;
  margin: 0;
  background: none;
  border: none;
  cursor: pointer;
  transform: rotate(-90deg);
  transition: .5s;
}
#backtop svg {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  bottom: -0.1vw;
}
.v-leave {
  opacity: 1;
}
.v-leave-active {
  transition: .5s
}
.v-leave-to {
  opacity: 0;
}
.v-enter {
  opacity: 0;
}
.v-enter-active {
  transition: .5s
}
.v-enter-to {
  opacity: 1;
}

@media (hover: hover) {
  #backtop:hover {
    transform: translate(0, -100%) rotate(-90deg);
  }
}

@media screen and (max-width: 480px) {
  .readbox {
    position: relative;
  }
  #btnet-logo img {
    width: 65px;
  }
  #backtop {
    font-size: 16px;
    right: -1em;
    bottom: 3em;
  }
}
</style>
