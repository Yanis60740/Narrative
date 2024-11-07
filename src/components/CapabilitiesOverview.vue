<template>
  <div class="capabilitiesOverview" ref="capabilitiesOverview">
    <div class="capabilitiesOverview__left">
      <p>WHAT WE CAN DO</p>
    </div>
    <div class="capabilitiesOverview__right">
      <div class="capabilitiesOverview__right__intro">
        <p>
          AFTER A DECADE OF WORKING FOR VARIOUS AMAZING COMPANIES AND<br>STUDIOS, I
          REALIZED THAT I WANTED MORE FREEDOM AND CREATIVE CONTROL<br>OVER MY WORK.
        </p>
        <p><br></p>

        <p>
          THAT'S WHEN I DECIDED TO TAKE THE LEAP AND START FREELANCING IN ORDER<br>
          TO BRING BOTH MY CLIENTS AND MY OWN VISIONS TO LIFE.
        </p>
      </div>
      <div class="capabilitiesOverview__right__subject">
        <span>EDITORIAL DESIGN</span>
        <div class="separator"></div>
        <span>3D AND MOTION</span>
        <div class="separator"></div>
        <span>PACKAGING</span>
        <div class="separator"></div>
        <span>BRAND IDENTIFITY</span>
        <div class="separator"></div>
        <span>DEVELOPMENT</span>
      </div>
    </div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
export default {
  name: "CapabilitiesOverview",
  data() {
    return {};
  },
  mounted() {
    this.appearOnScroll();
  },
  methods: {
    appearOnScroll() {
      const capabilitiesOverview = this.$refs.capabilitiesOverview
      gsap.to(capabilitiesOverview, {
        scrollTrigger: {
          trigger: ".capabilitiesOverview",
          start: "top 56%",
          end: "bottom 20%",
          toggleActions: "play none none none",
        },
        opacity: 1,
        duration: 1,
        ease: "power3.inOut",
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../css/global.scss";

.capabilitiesOverview {
  display: flex;
  height: min-content;
  overflow: hidden;
  padding: 120px 32px 0;
  position: relative;
  font-family: $inter;
  font-weight: 500;
  opacity: 0;
  color: var(--primary-text);
  &__left {
    display: flex;
    flex: 1 0 0px;
    height: min-content;
    overflow: hidden;
    position: relative;

    p {
      font-size: 12px;
      letter-spacing: -0.02em;
      line-height: 1.2em;
    }
  }

  &__right {
    display: flex;
    flex-direction: column;
    gap: 48px;

    &__intro {
      display: flex;
      flex-direction: column;
      gap: 23px;
      position: relative;

      p {
        font-size: 24px;
        line-height: 1.2em;
      }
    }

    &__subject {
      display: flex;
      flex-direction: column;
      width: 100%;
      height: 452px;

      span {
        display: flex;
        flex: 1 0 0px;
        align-items: center;
        padding: 16px;
      }
    }
  }
}

.separator {
  background-color: var(--primary-separator);
  flex: none;
  height: 1px;
  overflow: hidden;
  position: relative;
  width: 100%;
}
</style>
