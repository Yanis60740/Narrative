<template>
  <div class="nav" :class="themeClass">
    <div class="navbar">
      <div class="navbar__logo"><a>narrative</a></div>
      <div class="navbar__links">
        <div class="contact-container">
          <AnimSubtitle text="get in touch" />
        </div>
        <div class="switch-container" ref="switch" @mouseover="hoverSwitch" @mouseleave="unhoverSwitch" @click="handleClick">
          <div class="switch-container__sun" >
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 256" focusable="false"
              color="rgb(0, 0, 0)" style="
                user-select: none;
                width: 100%;
                height: 100%;
                display: inline-block;
                fill: var(
                  --token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb,
                  rgb(0, 0, 0)
                );
                color: var(
                  --token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb,
                  rgb(0, 0, 0)
                );
                flex-shrink: 0;
              ">
              <g color="var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(0, 0, 0))" weight="regular">
                <path
                  d="M120,40V16a8,8,0,0,1,16,0V40a8,8,0,0,1-16,0Zm72,88a64,64,0,1,1-64-64A64.07,64.07,0,0,1,192,128Zm-16,0a48,48,0,1,0-48,48A48.05,48.05,0,0,0,176,128ZM58.34,69.66A8,8,0,0,0,69.66,58.34l-16-16A8,8,0,0,0,42.34,53.66Zm0,116.68-16,16a8,8,0,0,0,11.32,11.32l16-16a8,8,0,0,0-11.32-11.32ZM192,72a8,8,0,0,0,5.66-2.34l16-16a8,8,0,0,0-11.32-11.32l-16,16A8,8,0,0,0,192,72Zm5.66,114.34a8,8,0,0,0-11.32,11.32l16,16a8,8,0,0,0,11.32-11.32ZM48,128a8,8,0,0,0-8-8H16a8,8,0,0,0,0,16H40A8,8,0,0,0,48,128Zm80,80a8,8,0,0,0-8,8v24a8,8,0,0,0,16,0V216A8,8,0,0,0,128,208Zm112-88H216a8,8,0,0,0,0,16h24a8,8,0,0,0,0-16Z">
                </path>
              </g>
            </svg>
          </div>
          <div class="switch-container__moon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 256" focusable="false" color="rgb(255, 255, 255)"
              style="user-select: none; width: 100%; height: 100%; display: inline-block; fill: var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(255, 255, 255)); color: var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(255, 255, 255)); flex-shrink: 0;">
              <g color="var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(0, 0, 0))" weight="regular">
                <path
                  d="M233.54,142.23a8,8,0,0,0-8-2,88.08,88.08,0,0,1-109.8-109.8,8,8,0,0,0-10-10,104.84,104.84,0,0,0-52.91,37A104,104,0,0,0,136,224a103.09,103.09,0,0,0,62.52-20.88,104.84,104.84,0,0,0,37-52.91A8,8,0,0,0,233.54,142.23ZM188.9,190.34A88,88,0,0,1,65.66,67.11a89,89,0,0,1,31.4-26A106,106,0,0,0,96,56,104.11,104.11,0,0,0,200,160a106,106,0,0,0,14.92-1.06A89,89,0,0,1,188.9,190.34Z">
                </path>
              </g>
            </svg>
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
        <div class="menu" v-for="(item, index) in listLeft" :key="index" :ref="'animmenu' + index">
          <div class="menu__box" :ref="'animmenu' + index">
            <AnimMenu :number="index + 1" :name="item.name" :ref="item.ref" />
          </div>
        </div>
      </div>
      <div class="navmenu__rightContent">
        <div class="navmenu__rightContent__link" v-for="(item, index) in listRight" :key="index"
          :ref="'animmenu' + index">
          <div class="navmenu__rightContent__link__box" :ref="'animmenu' + index">
            <span class="navmenu__rightContent__link__title">
              {{ item.title }}
            </span>
            <span class="navmenu__rightContent__link__content">
              <span v-if="index === 0">{{ item.content }}</span>
              <span v-else-if="typeof item.content === 'string'">
                <AnimSubtitle :text="item.content" />
              </span>
              <span class="social" v-else>
                <AnimSubtitle v-for="(subItem, subIndex) in item.content" :key="subIndex" :text="subItem" />
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
  name: "NavBar",
  components: {
    AnimSubtitle,
    AnimMenu,
  },
  inject: ["toggleTheme", "currentTheme"],
  data() {
    return {
      duration: 0.4,
      animMenuDuration: 0.4,
      listLeft: [
        { name: "HOME", url: "#" },
        { name: "ABOUT", url: "#" },
        { name: "WORKS", url: "#" },
        { name: "CONTACT", url: "#" },
      ],
      listRight: [
        { title: "LOCATION", content: "SQUARE, TASHKENT 10009, UZBEKISTAN" },
        { title: "EMAIL", content: "HELLO@SOMETHING.COM" },
        { title: "PHONE", content: "(307) 555-0133" },
        {
          title: "SOCIAL",
          content: ["BEHANCE", "INSTAGRAM", "DRIBBBLE", "SAVEE"],
        },
      ],
      isOpened: false,
      containerHeight: null,
      switch: false,
    };
  },
  mounted() {
    this.containerHeight = document
      .querySelector(".navmenu")
      .getBoundingClientRect().height;
    gsap.set(this.$refs.nav, { maxHeight: "0px" });
    gsap.set(this.$refs.nav, { padding: "0px" });
    this.initAnimation();
  },
  methods: {
    initAnimation() {
      this.tl = gsap.timeline({
        paused: true,
        onStart: () => console.log("start"),
        onComplete: () => console.log("complete"),
      });
      this.tl
        .to(this.$refs.nav, {
          maxHeight: this.containerHeight + "px",
          padding: "32px 0px",
          duration: this.duration,
          ease: "power3.inOut",
        })
        .fromTo(
          this.$refs.frame1,
          { rotation: 0, top: 11, left: 0 },
          {
            rotation: 45,
            top: 7,
            left: 7,
            duration: this.duration,
            ease: "power3.inOut",
          }
        )
        .fromTo(
          this.$refs.frame2,
          { rotation: 0, bottom: 11, left: 0 },
          {
            rotation: -45,
            bottom: 7,
            left: 7,
            duration: this.duration,
            ease: "power3.inOut",
          },
          "<"
        );

        let isFirstAnim = true;

      Object.keys(this.$refs).forEach((ref) => {
        if (ref.startsWith("animmenu")) {
          this.tl.fromTo(
            this.$refs[ref],
            { translateY: "92%", delay: 0.1, opacity: 0 },
            {
              translateY: "0%",
              delay: 0,
              opacity: 1,
              duration: this.animMenuDuration,
              ease: "power1.out",
              stagger: 0.1,
            }, isFirstAnim ? "<-0.3" : "<0.25"
          );
          isFirstAnim = false;
        }
      });
    },
    onclickMenu() {
      if (this.isOpened) {
        gsap.to(this.$refs.nav, {
          maxHeight: "0px",
          padding: "0px",
          duration: this.duration,
          ease: "power3.inOut",
          onComplete: () => {
            this.tl.pause().progress(0);
          },
        });
        const tl2 = gsap.timeline();
        tl2
          .fromTo(
            this.$refs.frame1,
            { rotation: 45, top: 7, left: 7 },
            {
              rotation: 0,
              top: 11,
              left: 0,
              duration: this.duration,
              ease: "power3.inOut",
            }
          )
          .fromTo(
            this.$refs.frame2,
            { rotation: -45, bottom: 7, left: 7 },
            {
              rotation: 0,
              bottom: 11,
              left: 0,
              duration: this.duration,
              ease: "power3.inOut",
            },
            "<"
          );
      } else {
        this.tl.play();
      }
      this.isOpened = !this.isOpened;
    },
    hoverSwitch() {
      gsap.to(
        this.$refs.switch,
        { scale: 1.1, duration: this.duration, ease: "power2.out" }
      );
    },
    unhoverSwitch() {
      gsap.to(
        this.$refs.switch,
        { scale: 1, duration: this.duration, ease: "power2.out" }
      );
    },
    handleClick() {
      this.toggleTheme();
      this.changeLogo();
    },
    changeLogo() {
      const sun = document.querySelector(".switch-container__sun");
      const moon = document.querySelector(".switch-container__moon");
      if (this.switch === false) {
        sun.style.opacity = "0";
        moon.style.opacity = "1";
      } else {
        sun.style.opacity = "1";
        moon.style.opacity = "0";
      }
      this.switch = !this.switch;
    },
  },
};
</script>
<!-- autoAlpha à la place de opacity // willchange -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "../css/global.scss";

.nav {
  display: flex;
  flex-direction: column;
  padding: 0px 32px;
  box-sizing: border-box;
  font-family: $inter;
  text-transform: uppercase;
  text-decoration: none;
  letter-spacing: -0.02em;
  line-height: 1.2em;
  overflow: hidden;
}

.navbar {
  height: 74px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: var(--primary-text);

  &__logo {
    font-weight: 600;
    font-size: $normal-size;
    display: flex;
    justify-content: center;
  }

  &__links {
    font-weight: 500;
    font-size: $small-size;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 24px;
  }
}

.contact-container {
  display: flex;
  justify-content: center;
  position: relative;
  width: 120px;
  cursor: pointer;
}

.switch-container {
  height: 40px;
  width: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  &__sun {
    position: absolute;
    height: 20px;
    width: 20px;
    opacity: 1;
  }
  &__moon {
    position: absolute;
    height: 20px;
    width: 20px;
    opacity: 0;
  }
}

.frame-box {
  position: relative;
  height: 32px;
  width: 32px;
  cursor: pointer;
}

.frame1 {
  flex: none;
  height: 1px;
  left: calc(50% - 24px / 2);
  overflow: hidden;
  position: absolute;
  top: 11px;
  width: 24px;
  background-color: var(--primary-text);
  transform: none;
  transform-origin: left center;
}

.frame2 {
  flex: none;
  height: 1px;
  left: calc(50% - 24px / 2);
  overflow: hidden;
  position: absolute;
  bottom: 11px;
  width: 24px;
  background-color: var(--primary-text);
  transform: none;
  transform-origin: left center;
}

.navmenu {
  display: flex;
  height: min-content;
  flex: 1 0 0px;
  background-color: var(--primary-bg);
  z-index: 2;
  position: absolute;
  width: 97%;
  top: 80px;
  box-sizing: "border-box";
  padding: 32px 32px;

  &__leftContent {
    display: flex;
    flex-direction: column;
    gap: 16px;
    flex: 1 0 0px;
  }

  &__rightContent {
    display: flex;
    flex-direction: column;
    gap: 32px;
    flex: 1 0 0px;
    color: var(--primary-text);
    &__link {
      overflow: hidden;

      &__box {
        transform: translate(0px, 92%);
        display: flex;
        flex-direction: column;
        gap: 16px;
        font-weight: 500;
        will-change: transform;
      }

      &__title {
        font-size: $paragraph-size;
      }

      &__content {
        font-size: $small-size;
        display: flex;
        gap: 24px;
      }
    }
  }
}

.social {
  display: flex;
  gap: 16px;
}

.menu {
  overflow: hidden;

  &__box {
    transform: translate(0px, 92%);
  }
}
</style>
