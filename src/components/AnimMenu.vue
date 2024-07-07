<template>
    <div class="animMenu" @mouseover="hover" @mouseleave="unhover">
      <div class="animMenu__number">0{{number}}</div>
      <div class="animMenu__name">{{name}}</div>
      <div class="animMenu__arrow" >
        <div class="animMenu__arrow__box" >
          <svg xmlns="http://www.w3.org/2000/svg" ref="animMenu" focusable="false" viewBox="0 0 24 24" color="var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(18, 18, 18))" style="user-select: none; width: 100%; height: 100%; display: inline-block; fill: var(--token-0819bdfd-ecdd-45ae-a012-dd02dc1d17eb, rgb(18, 18, 18)); flex-shrink: 0;"><path d="M12 4l-1.41 1.41L16.17 11H4v2h12.17l-5.58 5.59L12 20l8-8z"></path></svg>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import gsap from "gsap";
  export default {
    name: "AnimMenu",
    props: {
        number: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true
        }
    },
    data() {
      return {
          duration: 0.4
      };
    },
    mounted() {
      this.animationArrow = gsap.fromTo(
        this.$refs.animMenu,
        { x: -55 },
        {
          x: 0,
          duration: this.duration,
          ease: "power3.inOut",
          paused: true
        }
      );
    },
    methods: {
      hover() {
        this.animationArrow.play();
      },
      unhover() {
        this.animationArrow.reverse();
      },
    },
  };
  </script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.animMenu{
  display: flex;
  align-items: center;
  gap: 10px;
  width: min-content;
  cursor: pointer;
  font-size: 64px;
  font-family: "Inter-Medium", "Inter", "Inter Placeholder", sans-serif;
  font-weight: 500;
  letter-spacing: -0.02em;
  line-height: 1.2em;
  &__number{
    color: #ebebeb;
  }
  &__name{
    position: relative;
    color: black;
    background-color: white;
  }
  &__arrow{
    position: relative;
    width: 54px;
    overflow: hidden;
    &__box{
      display: flex;
      align-items: center;
      width: 54px;
      height: 54px;
    }
  }   
}

</style>