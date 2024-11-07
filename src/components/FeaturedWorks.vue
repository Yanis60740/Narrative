<template>
  <div class="featuredWorks" ref="featuredWorks">
    <div class="featuredWorks__title">
      <p>FEATURED WORKS</p>
    </div>
    <div class="featuredWorks__content">
        <AnimFeature :title="'KAIXIN SOYMILK'" :feature="'PACKAGING'" :img1="'/images/kaixin_soymilk1.jpg'" :img2="'/images/kaixin_soymilk2.jpg'" :img3="'/images/kaixin_soymilk3.jpg'"/>
        <AnimFeature :title="'DEPRESSION'" :feature="'BRANDING'" :img1="'/images/depression1.jpg'" :img2="'/images/depression2.jpg'" :img3="'/images/depression3.jpg'"/>
        <AnimFeature :title="'DOT STUDIO'" :feature="'PACKAGING & BRAND IDENTITY'" :img1="'/images/dot_studio1.jpg'" :img2="'/images/dot_studio2.jpg'" :img3="'/images/dot_studio3.jpg'"/>
        <AnimFeature :title="'LINE PEN'" :feature="'BRAND IDENTITY'" :img1="'/images/line_pen1.jpg'" :img2="'/images/line_pen2.jpg'" :img3="'/images/line_pen3.jpg'"/>
    </div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
import AnimFeature from './AnimFeature.vue';
export default {
  name: "FeaturedWorks",
  components: {
    AnimFeature
  },
  data() {
    return {
          duration: 0.4,
      };
  },
  mounted() {
    this.appearOnScroll();
  },
  methods: {
    appearOnScroll() {
      const featuredWorks = this.$refs.featuredWorks
      gsap.to(featuredWorks, {
        scrollTrigger: {
          trigger: ".featuredWorks",
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

.featuredWorks {
  display: flex;
  flex-direction: column;
  gap: 80px;
  height: min-content;
  overflow: hidden;
  padding: 120px 32px;
  box-sizing: border-box;
  font-family: $inter;
  font-weight: 500;
  opacity: 0;
  color: var(--primary-text);
  &__title {
    display: flex;
    p {
      font-size: 12px;
      letter-spacing: -0.02em;
      line-height: 1.2em;
    }
  }
  &__content {
    display: flex;
    width: 100%;
    flex-direction: column;
  }
}
</style>
