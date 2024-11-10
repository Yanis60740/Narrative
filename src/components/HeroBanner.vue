<template>
  <div class="heroBanner">
    <div class="titleContainer">
      <div class="titleContainer__title">
        <div v-for="(letter, index) in letters" :key="index" class="titleContainer__title__letterContainer"
          @mousemove="onMouseMove($event, index)" @mouseleave="onMouseLeave(index)">
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
              <div class="titleContainer__subtitle__right__subtitle__animContainer">
                <AnimSubtitle text="about us" />
              </div>
            </a>
          </div>
          <div class="titleContainer__subtitle__right__subtitle">
            <a>
              <div class="titleContainer__subtitle__right__subtitle__animContainer">
                <AnimSubtitle text="featured works" />
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="videoContainer">
      <div class="videoContainer__box">
        <div class="videoContainer__box__anim">
          <CustomCursor ref="customCursor" />
          <video src="/video/heroBanner.mp4" loop="" muted="" playsinline="" autoplay @mouseenter="onVideoEnter"
            @mouseleave="onVideoLeave"></video>
        </div>
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
      maxFontWeight: 1150, // Épaisseur maximale de la lettre
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
        ease: "power3.out",
      });
    },
    onMouseLeave(index) {
      // Réinitialiser la taille et l'épaisseur de la lettre avec GSAP lorsque le curseur quitte le conteneur
      gsap.to(this.$refs["letter" + index][0], {
        fontWeight: this.minFontWeight,
        duration: 0.3,
        ease: "power3.out",
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
  height: min-content;
  overflow: hidden;
  padding: 5px 32px 0;
  box-sizing: border-box;
  width: 100%;
  left: 0;
  top: 73px;
  font-family: $inter;

  &__title {
    position: relative;
    display: flex;
    cursor: default;
    white-space: pre;
    color: var(--primary-text);
    font-size: 124px;
    font-weight: 500;
    letter-spacing: -0.02em;
    line-height: 1em;

    &__letterContainer {
      position: relative;
    }
  }

  &__subtitle {
    align-items: center;
    display: flex;
    gap: 48px;
    height: min-content;
    overflow: hidden;
    font-family: "Inter-Medium", "Inter", "Inter Placeholder", sans-serif;
    color: var(--primary-text);
    font-size: $small-size;
    font-weight: 500;
    letter-spacing: -0.02em;
    line-height: 1.2em;
    text-transform: uppercase;
    &__left {
      display: flex;
      flex: 2 0 0px;
      gap: 32px;
      height: min-content;
      overflow: hidden;
    }

    &__right {
      display: flex;
      flex: 1 0 0px;
      gap: 16px;
      height: min-content;
      overflow: hidden;
      &__subtitle {
        a {
          cursor: pointer;
          display: flex;
          gap: 4px;
          height: 22px;
          text-decoration: none;
        }

        &__animContainer {
          display: flex;
          gap: 10px;
          height: 20px;
          overflow: hidden;
          font-family: "Inter-Medium", "Inter", "Inter Placeholder", sans-serif;
          color: var(--primary-text);
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
  display: flex;
  gap: 10px;
  height: 748px;
  overflow: hidden;
  padding: 24px 32px 39px;
  font-family: $inter;
  &__box {
    cursor: pointer;
    flex: 1 0 0px;
    height: 100%;
    overflow: hidden;
    position: relative;
    width: 1px;
    &__anim {
      height: 100%;
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
        object-position: 50% 50%;
      }
    }
  }
}
</style>
