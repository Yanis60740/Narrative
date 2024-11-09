<template>
    <div class="loadingScreen" ref="screen" v-if="isLoading">
        <div class="loadingScreen__container">
            <div class="loadingScreen__container__box">
                <div class="loadingScreen__container__box__studio" ref="studio">
                    studio
                </div>
                <div class="loadingScreen__container__box__narrative" ref="narrative">
                    narrative
                </div>
            </div>
            <div class="loadingScreen__container__bar" ref="barContainer">
                <div class="loadingScreen__container__bar__fill" ref="bar"></div>
            </div>
        </div>
    </div>
</template>

<script>
import { gsap } from "gsap";
export default {
    name: "LoadingScreen",
    data() {
        return {
            isLoading: true,
            // tl : null,
        };
    },
    mounted() {
        this.animation();
        // Simulate a load time (e.g., for testing)
        // setTimeout(() => {
        // this.isLoading = false;
        // this.$emit("loaded"); // Notify the parent component
        // }, 3000); // Adjust this timeout as needed
    },
    methods: {
        animation() {
            gsap.set(this.$refs.studio, { yPercent: 100 });
            gsap.set(this.$refs.narrative, { yPercent: 100 });
            this.tl = gsap.timeline();
            this.tl
                .fromTo(this.$refs.bar, {
                    width: "0%",
                }, {
                    width: "3%",
                    duration: 0.2,
                    ease: "power3.inOut",
                })
                .fromTo(this.$refs.bar, {
                    width: "3%",
                }, {
                    width: "100%",
                    duration: 0.8,
                    ease: "power3.in",
                }, "<0.8")
                .to(this.$refs.studio, {
                    duration: 0.5,
                    yPercent: -10,
                    ease: "power4.inOut",
                }, "<0.1")
                .to(this.$refs.narrative,{
                        duration: 0.5,
                        yPercent: -10,
                        ease: "power4.inOut",
                },"<0.1")
                .to(this.$refs.studio, {
                    duration: 0.4,
                    yPercent: 0,
                    ease: "power3.inOut",
                }, "<0.3")
                .to(this.$refs.narrative,{
                    duration: 0.4,
                    yPercent: 0,
                    ease: "power3.inOut",
                }, "<0.1")
                .to(
                    this.$refs.studio,
                    {
                        duration: 0.5,
                        yPercent: -100,
                        ease: "power3.inOut",
                    },
                    "<1.5"
                )
                .to(
                    this.$refs.narrative,
                    {
                        duration: 0.5,
                        yPercent: -100,
                        ease: "power3.inOut",
                    },
                    "<0.1"
                )
                .to(this.$refs.barContainer, {
                    opacity: "0",
                    duration: 0.6,
                    ease: "power2.inOut",
                }, "<-0.1")
                .to(this.$refs.screen, {
                    height: "0",
                    duration: 0.6,
                    ease: "power3.inOut",
                }, "<0.4");

        },
    },
};
</script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.loadingScreen {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background-color: var(--primary-bg);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;

    &__container {
        display: flex;
        flex-direction: column;
        gap: 16px;

        &__box {
            display: flex;
            gap: 16px;
            font-family: $inter;
            font-size: 48px;
            text-transform: uppercase;
            font-weight: 500;
            overflow: hidden;
        }

        &__bar {
            align-self: stretch;
            height: 2px;
            overflow: hidden;
            position: relative;
            background-color: var(--primary-opacity);

            &__fill {
                width: 0;
                height: 4px;
                position: absolute;
                // top: calc(50.00000000000002% - 4px / 2);
                background-color: var(--primary-text);
            }
        }
    }
}
</style>
