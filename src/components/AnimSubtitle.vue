<template>
    <div class=animSubtitle  @mouseover="hover" @mouseleave="unhover">
        <p class="firstSpan" ref="firstSp">{{ text }}</p>
        <p :class="['secondSpan', customClass]" ref="secondSp">{{ text }}</p>
    </div>
  </template>
  
  <script>
  import gsap from "gsap";
  export default {
    name: "AnimSubtitle",
    props: {
        text: {
            type: String,
            required: true
        },
        customClass: {
      type: String,
      default: "",
    },
    },
    data() {
      return {
          duration: 0.4,
      };
    },
    methods: {
      hover() {
        gsap.to(this.$refs.firstSp, {
          yPercent: "-100",
          duration: this.duration,
          // delay: 1,
          opacity: 0,
          ease: "power3.inOut",
        });
        gsap.to(this.$refs.secondSp, {
          yPercent: "-100",
          duration: this.duration,
          opacity: 1,
          ease: "power3.inOut",
        });
        
      },
      unhover() {
        gsap.to(this.$refs.firstSp, {
          yPercent: "0",
          duration: this.duration,
          // delay: 0.17,
          opacity: 1,
          ease: "power3.inOut",
        });
        gsap.to(this.$refs.secondSp, {
          yPercent: "0",
          duration: this.duration,
          // delay: 0.26,
          opacity: 0,
          ease: "power3.inOut",
        });
      },
    },
  };
  </script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.animSubtitle{
  position: relative;
  display: flex;
  justify-content: center;
  flex-direction: column; 
  overflow: hidden;
  cursor: pointer;
}
.secondSpan{
  position: absolute;
  transform: translateY(100%);
  opacity: 0;
}
</style>