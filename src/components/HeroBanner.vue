<template>
  <div class="titleContainer">
    <div class="titleContainer__title">
      <div
        v-for="(letter, index) in letters"
        :key="index"
        class="titleContainer__title__letterContainer"
        @mousemove="onMouseMove($event, index)"
        @mouseleave="onMouseLeave(index)"
      >
        <span :ref="'letter' + index" class="letter">{{ letter }}</span>
      </div>
    </div>
    <div class="titleContainer__subtitle">
      <div class="titleContainer__subtitle__left">
        <div>
          <p>STUDIO NARRATIVE</p>
        </div>
        <div>
          <p>Award winning digital studio Based Tashkent</p>
        </div>
      </div>
      <div class="titleContainer__subtitle__right">
        <div class="titleContainer__subtitle__right__subtitle">
          <a>
            <div
              class="titleContainer__subtitle__right__subtitle__animContainer"
            >
              <AnimSubtitle text="about us" />
            </div>
          </a>
        </div>
        <div class="titleContainer__subtitle__right__subtitle">
          <a>
            <div
              class="titleContainer__subtitle__right__subtitle__animContainer"
            >
              <AnimSubtitle text="featured works" />
            </div>
          </a>
        </div>
      </div>
    </div>
  </div>
  <div class="videoContainer">
    
    <div class="videoContainer__box" >
      <div class="videoContainer__box__anim">
        <CustomCursor ref="customCursor" />
        <video
          src="/video/heroBanner.mp4"
          loop=""
          muted=""
          playsinline=""
          autoplay
          @mouseenter="onVideoEnter"
          @mouseleave="onVideoLeave"
        ></video>
      </div>
    </div>
  </div>
</template>

<script>
import AnimSubtitle from "./AnimSubtitle.vue";
import CustomCursor from './CustomCursor.vue';
import gsap from "gsap";

export default {
  name: "HeroBanner",
  components: {
    AnimSubtitle,
    CustomCursor
  },
  data() {
    return {
      duration: 0.4,
      maxFontWeight: 900, // Épaisseur maximale de la lettre
      minFontWeight: 500, // Épaisseur minimale de la lettre
      letters: ["N", "A", "R", "R", "A", "T", "I", "V", "E"],
    };
  },
  methods: {
    onMouseMove(event, index) {
      const rect = this.$refs["letter" + index][0].getBoundingClientRect();
      const x = event.clientX - rect.left; // Position x du curseur par rapport au conteneur
      const y = event.clientY - rect.top; // Position y du curseur par rapport au conteneur
      const centerX = rect.width / 2;
      const centerY = rect.height / 2;

      // Calculer la distance entre le curseur et le centre de la lettre
      const distance = Math.sqrt((x - centerX) ** 2 + (y - centerY) ** 2);
      const maxDistance = Math.sqrt(centerX ** 2 + centerY ** 2);

      // Calculer le pourcentage de la distance
      const distancePercentage = Math.min(distance / maxDistance, 1);

      // Calculer la taille et l'épaisseur de la lettre en fonction de la distance
      const fontWeight =
        this.minFontWeight +
        (1 - distancePercentage) * (this.maxFontWeight - this.minFontWeight);

      // Mettre à jour les styles de la lettre avec GSAP
      gsap.to(this.$refs["letter" + index][0], {
        fontWeight: fontWeight,
        duration: 0.1,
        ease: "power1.out",
      });
    },
    onMouseLeave(index) {
      // Réinitialiser la taille et l'épaisseur de la lettre avec GSAP lorsque le curseur quitte le conteneur
      gsap.to(this.$refs["letter" + index][0], {
        fontWeight: this.minFontWeight,
        duration: 0.3,
        ease: "power1.out",
      });
    },
    onVideoEnter() {
      this.$refs.customCursor.setCursorText('PLAY'); // Afficher un texte dans le curseur au survol de la vidéo
    },
    onVideoLeave() {
      this.$refs.customCursor.resetCursorText(); // Réinitialiser le texte en quittant la vidéo
    }
  },
};
</script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.titleContainer {
  display: flex;
  flex-direction: column;
  gap: 10px;
  height: -moz-min-content;
  height: min-content;
  justify-content: center;
  overflow: hidden;
  padding: 5px 32px 0;
  // position: absolute;
  width: 100%;
  left: 0;
  top: 73px;
  font-family: $inter;
  &__title {
    position: relative;
    display: flex;
    cursor: default;
    white-space: pre;
    color: black;
    font-size: 124px;
    font-weight: 500;
    letter-spacing: -0.02em;
    line-height: 1em;
    &__letterContainer {
      position: relative;
    }
  }

  &__subtitle {
    align-content: center;
    align-items: center;
    display: flex;
    flex: none;
    flex-direction: row;
    flex-wrap: nowrap;
    gap: 48px;
    height: min-content;
    justify-content: center;
    overflow: hidden;
    padding: 0;
    position: relative;
    width: 100%;

    &__left {
      align-content: center;
      align-items: center;
      display: flex;
      flex: 2 0 0px;
      flex-direction: row;
      flex-wrap: nowrap;
      gap: 32px;
      height: min-content;
      justify-content: flex-start;
      overflow: hidden;
      padding: 0;
      position: relative;
      width: 1px;

      div {
        outline: none;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        flex-shrink: 0;
        transform: none;

        p {
          font-family: "Inter-Medium", "Inter", "Inter Placeholder", sans-serif;
          color: black;
          font-size: $small-size;
          font-weight: 500;
          letter-spacing: -0.02em;
          line-height: 1.2em;
          text-transform: uppercase;
        }
      }
    }

    &__right {
      align-content: center;
      align-items: center;
      display: flex;
      flex: 1 0 0px;
      flex-direction: row;
      flex-wrap: nowrap;
      gap: 16px;
      height: min-content;
      justify-content: flex-start;
      overflow: hidden;
      padding: 0;
      position: relative;

      &__subtitle {
        a {
          align-content: center;
          align-items: center;
          cursor: pointer;
          display: flex;
          flex-direction: column;
          flex-wrap: nowrap;
          gap: 4px;
          height: 22px;
          justify-content: center;
          overflow: visible;
          padding: 0;
          position: relative;
          text-decoration: none;
        }

        &__animContainer {
          align-content: flex-start;
          align-items: flex-start;
          display: flex;
          flex: none;
          flex-direction: column;
          flex-wrap: nowrap;
          gap: 10px;
          height: 20px;
          justify-content: flex-start;
          overflow: hidden;
          padding: 0;
          position: relative;
          z-index: 1;
          font-family: "Inter-Medium", "Inter", "Inter Placeholder", sans-serif;
          color: black;
          font-size: $small-size;
          font-weight: 500;
          letter-spacing: -0.02em;
          line-height: 1.2em;
          text-transform: uppercase;
        }
      }
    }
  }
}

.letter {
  transition: font-size 0.1s, font-weight 0.1s;
}

.videoContainer {
  align-content: center;
  align-items: center;
  display: flex;
  flex: none;
  flex-direction: row;
  flex-wrap: nowrap;
  gap: 10px;
  height: 748px;
  justify-content: center;
  overflow: hidden;
  padding: 24px 32px 39px;
  position: relative;
  // transform: perspective(1200px);
  width: 100%;
  font-family: $inter;
  &__box {
    cursor: pointer;
    flex: 1 0 0px;
    height: 100%;
    overflow: hidden;
    position: relative;
    width: 1px;

    &__anim {
      flex: none;
      height: 100%;
      // left: calc(50.00000000000002% - 100% / 2);
      position: absolute;
      top: 0;
      width: 100%;

      video {
        cursor: none;
        width: 100%;
        height: 100%;
        border-radius: 0px;
        display: block;
        object-fit: cover;
        background-color: rgb(235, 235, 235);
        object-position: 50% 50%;
      }
    }
  }
}
</style>
