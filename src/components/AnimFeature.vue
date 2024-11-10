<template>
  <div class="animFeature" @mouseover="hover" @mouseleave="unhover">
    <div class="animFeature__title" ref="titleFeature">{{ title }}</div>
    <div class="animFeature__animation" ref="boxFeature">
      <div class="animFeature__animation__title" ref="feature">
        {{ feature }}
      </div>
      <div class="animFeature__animation__box">
        <div class="animFeature__animation__box__images">
          <div class="animFeature__animation__box__images__box1" ref="img1">
            <div class="frame">
              <img :src="img1" :alt="title" />
            </div>
          </div>
          <div class="animFeature__animation__box__images__box2" ref="img2">
            <div class="frame">
              <img :src="img2" :alt="title" />
            </div>
          </div>
          <div class="animFeature__animation__box__images__box3" ref="img3">
            <div class="frame">
              <img :src="img3" :alt="title" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
export default {
  name: "AnimFeature",
  props: {
    title: {
      type: String,
      required: true,
    },
    feature: {
      type: String,
      required: true,
    },
    img1: {
      type: String,
      required: true,
    },
    img2: {
      type: String,
      required: true,
    },
    img3: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      duration: 0.6,
      CustomEase: "M0,0 C0,1 0,1 1,1 ",
    };
  },
  methods: {
    hover() {
      let responsive = gsap.matchMedia();
      responsive.add("(min-width: 1200px)", () => {
        this.tlEnter = gsap.timeline({ overwrite: "auto" });
        this.tlEnter
          .to(
            this.$refs.boxFeature,
            {
              duration: this.duration,
              ease: this.CustomEase,
              height: "124px",
            },
            0.1
          )
          .to(
            this.$refs.feature,
            {
              yPercent: -100,
              duration: this.duration,
              ease: this.CustomEase,
            },
            0.1
          )
          .to(
            this.$refs.img1,
            {
              bottom: "0px",
              duration: this.duration,
              ease: this.CustomEase,
            },
            0.1
          )
          .to(
            this.$refs.img2,
            {
              bottom: "0px",
              duration: this.duration,
              ease: this.CustomEase,
            },
            "<"
          )
          .to(
            this.$refs.img3,
            {
              bottom: "0px",
              duration: this.duration,
              ease: this.CustomEase,
            },
            "<"
          )
          .to(
            this.$refs.boxFeature,
            {
              duration: this.duration,
              ease: this.CustomEase,
              justifyContent: "flex-end",
            },
            0.3
          );
      });

      responsive.add("(max-width: 1199px)", () => {
        gsap.to(
          this.$refs.titleFeature,
          {
            xPercent: 10,
            duration: this.duration,
            ease: this.CustomEase,
          }
        )
      });
    },
    unhover() {
      let responsive = gsap.matchMedia();
      responsive.add("(min-width: 1200px)", () => {
        this.tlLeave = gsap.timeline();
        this.tlLeave
          .to(
            this.$refs.img3,
            {
              bottom: "-270px",
              duration: this.duration,
              ease: this.CustomEase,
            },
            0.1
          )
          .to(
            this.$refs.img2,
            {
              bottom: "-240px",
              duration: this.duration,
              ease: this.CustomEase,
            },
            "<"
          )
          .to(
            this.$refs.img1,
            {
              bottom: "-174px",
              duration: this.duration,
              ease: this.CustomEase,
            },
            "<"
          )
          .to(
            this.$refs.boxFeature,
            {
              duration: this.duration,
              ease: this.CustomEase,
              justifyContent: "flex-start",
            },
            0.4
          )
          .to(
            this.$refs.feature,
            {
              yPercent: 0,
              duration: this.duration,
              ease: this.CustomEase,
            },
            0.1
          )
          .to(
            this.$refs.boxFeature,
            {
              duration: this.duration,
              ease: this.CustomEase,
              height: "30px",
            },
            "<"
          );
      });
      responsive.add("(max-width: 1199px)", () => {
        gsap.to(
          this.$refs.titleFeature,
          {
            xPercent: 0,
            duration: this.duration,
            ease: this.CustomEase,
          }
        )
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.animFeature {
  align-items: center;
  cursor: pointer;
  display: flex;
  height: 236px;
  justify-content: space-between;
  overflow: hidden;
  padding: 80px 64px;
  position: relative;
  text-decoration: none;
  box-sizing: border-box;

  &__title {
    display: flex;
    justify-content: center;
    font-size: 64px;
    letter-spacing: -0.02em;
  }

  &__animation {
    align-items: flex-end;
    display: flex;
    flex-direction: column;
    gap: 10px;
    height: 30px;
    overflow: hidden;
    position: relative;
    width: min-content;

    &__title {
      font-size: 24px;
      letter-spacing: -0.02em;
    }

    &__box {
      flex: none;
      height: auto;
      position: relative;
      width: auto;

      &__images {
        height: 124px;
        overflow: hidden;
        position: relative;
        width: 404px;

        :nth-child(2) {
          left: calc(50.00000000000002% - 124px / 2);
        }

        :nth-child(3) {
          right: 0;
        }

        &__box1 {
          bottom: -174px;
          height: 124px;
          overflow: hidden;
          position: absolute;
          width: 124px;
        }

        &__box2 {
          bottom: -240px;
          height: 124px;
          overflow: hidden;
          position: absolute;
          width: 124px;
        }

        &__box3 {
          bottom: -270px;
          height: 124px;
          overflow: hidden;
          position: absolute;
          width: 124px;
        }
      }
    }
  }
}

.frame {
  position: absolute;
  border-radius: inherit;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  img {
    display: block;
    width: 124px;
    height: 124px;
    border-radius: inherit;
    object-position: center;
    object-fit: cover;
    image-rendering: auto;
  }
}
</style>
