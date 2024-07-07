<template>
    <div class="animSubtitle"  @mouseover="hover" @mouseleave="unhover">
        <span class="firstSpan" ref="firstSp">{{ text }}</span>
        <span class="secondSpan" ref="secondSp">{{ text }}</span>
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
        }
    },
    data() {
      return {
          duration: 0.4,
      };
    },
    methods: {
      hover() {
        gsap.to(this.$refs.firstSp, {
          translateY: "-110%",
          duration: this.duration,
          // delay: 1,
          opacity: 0,
          ease: "power3.inOut",
        });
        gsap.to(this.$refs.secondSp, {
          translateY: "0%",
          duration: this.duration,
          opacity: 1,
          ease: "power3.inOut",
        });
        
      },
      unhover() {
        gsap.to(this.$refs.firstSp, {
          translateY: "0%",
          duration: this.duration,
          // delay: 0.17,
          opacity: 1,
          ease: "power3.inOut",
        });
        gsap.to(this.$refs.secondSp, {
          translateY: "110%",
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
  transform: translateY(110%);
  color: black;
  opacity: 0;
}
</style>