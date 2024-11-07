<template>
  <div class="aboutUs" ref="aboutUs">
    <div class="aboutUs__textContainer">
      <p class="sentence">
        <span v-for="(word, wordIndex) in words" :key="wordIndex" class="word">
      <span
        v-for="(letter, letterIndex) in word"
        :key="letterIndex"
        class="letter"
        :ref="'letter' + (letterIndex + totalIndex(wordIndex))"
      >
        {{ letter }}
      </span>
      <!-- Ajouter un espace après chaque mot sauf le dernier -->
      <span v-if="wordIndex < words.length - 1">&nbsp;</span>
    </span>
      </p>
    </div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
export default {
  name: "AboutUs",
  data() {
    return {
      text: "WE ARE A SEASONED DIGITAL AGENCY HEADQUARTERED IN TASHKENT, BOASTING OVER 15 YEARS OF EXPERTISE.  OUR PASSION LIES IN CRAFTING DISTINCTIVE DIGITAL EXPERIENCES THAT CAPTIVATE AND RESONATE WITH AUDIENCES.",
      letters: []
    };
  },
  computed: {
    words() {
      return this.text.split(" ").map((word) => word.split(""));
    },
  },
  mounted() {
    this.animateTextOnScroll();
    this.appearOnScroll();
  },
  methods: {
    appearOnScroll() {
      const aboutUs = this.$refs.aboutUs

      gsap.to(aboutUs, {
        scrollTrigger: {
          trigger: ".aboutUs",
          start: "top 85%",
          end: "bottom 20%",
          toggleActions: "play none none none",
        },
        opacity: 1,
        duration: 0.6,
        ease: "power3.inOut",
      });
    },
    totalIndex(wordIndex) {
      return this.words
        .slice(0, wordIndex)
        .reduce((acc, word) => acc + word.length, 0);
    },
    
    animateTextOnScroll() {
      const letters = this.$refs;
      const letterRefs = Object.values(letters);

      gsap.to(letterRefs, {
        scrollTrigger: {
          trigger: ".sentence",
          start: "top 60%",
          end: "+=510",
          scrub: true,
        },
        opacity: 1,
        stagger: {
          each: 0.5,
          from: "start",
        },
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../css/global.scss";

.aboutUs {
  display: flex;
  gap: 10px;
  height: min-content;
  overflow: hidden;
  padding: 0 32px;
  position: relative;
  opacity: 0;
  .aboutUs__textContainer {
    flex: 1 0 0px;
    height: auto;
    position: relative;
    width: 1px;
    .sentence {
      font-family: $inter;
      font-size: 48px;
      font-style: normal;
      font-weight: 600;
      line-height: 1.4em;
      display: flex;
      flex-wrap: wrap;
      color: var(--primary-text);
    }
  }
}
.letter {
  display: inline-block;
   /* Transition fluide */
  opacity: 0.1;
}

</style>
