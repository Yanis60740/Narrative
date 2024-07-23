<template>
  <div class="nav">
    <div class="navbar">
      <div class="navbar__logo"><a>narrative</a></div>
      <div class="navbar__links">
        <div class="contact-container"><AnimSubtitle text="get in touch"/></div>
        <div class="sun-container" @mouseover="hoverSun" @mouseleave="unhoverSun">
          <div class="sun-container__element">
            <svg xmlns="http://www.w3.org/2000/svg" ref="sun" viewBox="0 0 256 256" focusable="false" color="var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(0, 0, 0))" style="user-select: none; width: 100%; height: 100%; display: inline-block; fill: var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(0, 0, 0)); color: var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(0, 0, 0)); flex-shrink: 0;"><g color="var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(0, 0, 0))" weight="regular"><path d="M120,40V16a8,8,0,0,1,16,0V40a8,8,0,0,1-16,0Zm72,88a64,64,0,1,1-64-64A64.07,64.07,0,0,1,192,128Zm-16,0a48,48,0,1,0-48,48A48.05,48.05,0,0,0,176,128ZM58.34,69.66A8,8,0,0,0,69.66,58.34l-16-16A8,8,0,0,0,42.34,53.66Zm0,116.68-16,16a8,8,0,0,0,11.32,11.32l16-16a8,8,0,0,0-11.32-11.32ZM192,72a8,8,0,0,0,5.66-2.34l16-16a8,8,0,0,0-11.32-11.32l-16,16A8,8,0,0,0,192,72Zm5.66,114.34a8,8,0,0,0-11.32,11.32l16,16a8,8,0,0,0,11.32-11.32ZM48,128a8,8,0,0,0-8-8H16a8,8,0,0,0,0,16H40A8,8,0,0,0,48,128Zm80,80a8,8,0,0,0-8,8v24a8,8,0,0,0,16,0V216A8,8,0,0,0,128,208Zm112-88H216a8,8,0,0,0,0,16h24a8,8,0,0,0,0-16Z"></path></g></svg>
          </div>
        </div>
        <div class="frame-box" @click="onclickMenu">
          <div class="frame1" ref="frame1"></div>
          <div class="frame2" ref="frame2"></div>
        </div>
      </div>
    </div>
    <div class="navmenu" ref="nav">
      <div class="navmenu__leftContent">        
        <div class="menu" 
        v-for="(item, index) in listLeft" 
          :key="index" 
          :ref="'animmenu' + index">
          <div class="menu__box" :ref="'animmenu' + index">     
            <AnimMenu :number="index + 1" :name="item.name" :ref="item.ref"/>
          </div>
        </div>
      </div>
      <div class="navmenu__rightContent">
        <div class="navmenu__rightContent__link"
        v-for="(item, index) in listRight" 
          :key="index" 
          :ref="'animmenu' + index">
          <div class="navmenu__rightContent__link__box" :ref="'animmenu' + index">
            <span class="navmenu__rightContent__link__title">
              {{item.title}}
            </span>
            <span class="navmenu__rightContent__link__content">
              <span v-if="index === 0">{{ item.content }}</span>
              <span v-else-if="typeof item.content === 'string'">
                <AnimSubtitle :text="item.content"/>
              </span>
              <span class="social" v-else>
                <AnimSubtitle v-for="(subItem, subIndex) in item.content" :key="subIndex" :text="subItem"/>
              </span>
            </span>
          </div>
        </div>
      </div>
    </div>
</div>
</template>

<script>
import AnimSubtitle from "./AnimSubtitle.vue";
import AnimMenu from "./AnimMenu.vue";
import gsap from "gsap";

export default {
  name: 'NavBar',
  components: {
    AnimSubtitle,
    AnimMenu
  },
  data() {
    return {
      duration: 0.4,
      animMenuDuration: 0.2,
      listLeft: [
        { name: "HOME", url: "#" },
        { name: "ABOUT", url: "#" },
        { name: "WORKS", url: "#" },
        { name: "CONTACT", url: "#" }
      ],
      listRight: [
        { title: "LOCATION", content: "SQUARE, TASHKENT 10009, UZBEKISTAN" },
        { title: "EMAIL", content: "HELLO@SOMETHING.COM" },
        { title: "PHONE", content: "(307) 555-0133" },
        { title: "SOCIAL", content: ["BEHANCE", "INSTAGRAM", "DRIBBBLE", "SAVEE"] }
      ],
      isOpened: false,
      // tl: null // Pour stocker la timeline GSAP
    };
  },
  mounted() {
    this.initAnimation();
  },
  methods: {
    initAnimation() {
      this.tl = gsap.timeline({ paused: true });
      this.tl
        .fromTo(
          this.$refs.frame1,
          { rotation: 0, top: 11, left: 0 },
          { rotation: 45, top: 7, left: 7, duration: this.duration, ease: "power3.inOut" }
        )
        .fromTo(
          this.$refs.frame2,
          { rotation: 0, bottom: 11, left: 0 },
          { rotation: -45, bottom: 7, left: 7, duration: this.duration, ease: "power3.inOut" },
          "<"
        )
        .fromTo(
          this.$refs.nav,
          { maxHeight: "130px" },
          { maxHeight: "1000vh", duration: this.duration, ease: "power3.inOut" },
        )
        Object.keys(this.$refs).forEach(ref => {
          if (ref.startsWith('animmenu')) {
            this.tl.fromTo(
              this.$refs[ref],
              { translateY: "92%", delay: 0.2 },
              { translateY: "0%", delay: 0, duration: this.animMenuDuration, ease: "power1.out" },
               // "<" synchronise les animations sans décalage
            );
          }
        });
    },
    onclickMenu() {
      if (this.isOpened) {
        this.tl.reverse();
      } else {
        this.tl.play();
      }
      this.isOpened = !this.isOpened;
    },
    hoverSun() {
      gsap.fromTo(
        this.$refs.sun,
        { scale: 1.1 },
        { scale: 1, duration: this.duration, ease: "power2.out" }
      );
    },
    unhoverSun() {
      gsap.fromTo(
        this.$refs.sun,
        { scale: 1 },
        { scale: 1.1, duration: this.duration, ease: "power2.out" }
      );
    }
  }
};
</script>
<!-- autoAlpha à la place de opacity // willchange -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "../css/global.scss";

.nav{
  display: flex;
  flex-direction: column;
  padding: 0px 32px;
  box-sizing: border-box;
  gap: 32px;
  font-family: "Inter";
  text-transform: uppercase;
  text-decoration: none;
  letter-spacing: -.02em;
  line-height: 1.2em;
  // z-index: 10;
  
  overflow: hidden;
  background-color: yellowgreen
}

.navbar{
  height: 74px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  // z-index: 3;
  &__logo{
    font-weight: 600;
    font-size: $normal-size;
    display: flex;
    justify-content: center;
  }
  &__links{
    font-weight: 500;
    font-size: $small-size;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 24px;
  }
}

.contact-container{
  display: flex;
  justify-content: center;
  position: relative;
  width: 120px;
  cursor: pointer;
}

.sun-container{
  height: 40px;
  width: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  &__element{
    height: 20px;
    width: 20px;
  }
}

.frame-box{
  position: relative;
  height: 32px;
  width: 32px;
  cursor: pointer;
}

.frame1{
  flex: none;
  height: 1px;
  left: calc(50% - 24px / 2);
  overflow: hidden;
  position: absolute;
  top: 11px;
  width: 24px;
  background-color: black;
  transform: none;
  transform-origin: left center;
}

.frame2{
  flex: none;
  height: 1px;
  left: calc(50% - 24px / 2);
  overflow: hidden;
  position: absolute;
  bottom: 11px;
  width: 24px;
  background-color: black;
  transform: none;
  transform-origin: left center;
}

.navmenu{
  display: flex;
  height: min-content;
  // z-index: 2;
  flex: 1 0 0px;
  &__leftContent{
    display: flex;
    flex-direction: column;
    gap: 16px;
    flex: 1 0 0px;
  }
  &__rightContent{
    display: flex;
    flex-direction: column;
    gap: 32px;
    flex: 1 0 0px;
    &__link{
      overflow: hidden;
      &__box{
        transform: translate(0px, 92%);
        display: flex;
        flex-direction: column;
        gap: 16px;
        font-weight: 500;
        will-change: transform;
      }
      &__title{
        font-size: $paragraph-size;
      }
      &__content{
        font-size: $small-size;
        display: flex;
        gap: 24px;
      }
    }
  }
}

.social{
  display: flex;
  gap: 16px;
}

.menu{
  overflow: hidden;
  &__box{
    transform: translate(0px, 92%);
  }
}  
</style>
