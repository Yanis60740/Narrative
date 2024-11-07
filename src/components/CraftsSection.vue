<template>
  <div class="craftsSection" ref="craftsSection">
    <div class="craftsSection__title">
      <p>CRAFTS</p>
    </div>
    <div class="craftsSection__content">
      <div class="craftsSection__content__box">
        <div class="craftsSection__content__box__carrousel">
          <div v-for="(item, index) in items" :key="index">
            <div class="carrousel-item">
              <img :src="item" />
            </div>
          </div>
        </div>
        <div class="craftsSection__content__box__carrousel" aria-hidden="true">
          <div v-for="(item, index) in items" :key="index">
            <div class="carrousel-item">
              <img :src="item" />
            </div>
          </div>
        </div>
        <div class="craftsSection__content__box__carrousel" aria-hidden="true">
          <div v-for="(item, index) in items" :key="index">
            <div class="carrousel-item">
              <img :src="item" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);
export default {
  data() {
    return {
      items: [
        "/images/caroussel1.jpg",
        "/images/caroussel2.jpg",
        "/images/caroussel3.jpg",
        "/images/caroussel4.jpg",
      ],
      carrouselWidth: null,
    };
  },
  mounted() {
    this.appearOnScroll();
    this.startCarouselCrafts();
  },
  methods: {
    appearOnScroll() {
      const craftsSection = this.$refs.craftsSection;
      gsap.to(craftsSection, {
        scrollTrigger: {
          trigger: ".craftsSection",
          start: "top 60%",
          end: "bottom 20%",
          toggleActions: "play none none none",
        },
        opacity: 1,
        duration: 1,
        ease: "power3.inOut",
      });
    },
    startCarouselCrafts() {
      const carrouselWidth = document.querySelector(".craftsSection__content__box__carrousel").offsetWidth;
        gsap.set(".craftsSection__content__box__carrousel", {
          x: (i) => i * (carrouselWidth +10),
          left: -carrouselWidth,
        });
        gsap.to(".craftsSection__content__box__carrousel", {
          duration: 50,
          ease: "none",
          x: `+=` + ((carrouselWidth * 3) + 30),
          modifiers: {
            x: gsap.utils.unitize(x => parseFloat(x) % ((carrouselWidth * 3) +30)),
          },
          repeat: -1
        });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.craftsSection {
  display: flex;
  flex-direction: column;
  gap: 80px;
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
    height: 364px;
    overflow: hidden;
    &__box {
      display: flex;
      position: relative;
      &__carrousel {
        display: flex;
        gap: 10px;
        position: absolute;
      }
      .carrousel-item {
        height: 364px;
        width: 364px;
        img {
          display: block;
          width: 100%;
          height: 100%;
          object-fit: cover;
          image-rendering: auto;
        }
      }
    }
  }
}
</style>
