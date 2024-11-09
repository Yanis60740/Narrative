<template>
    <div class="footerNarrative">
        <div class="footerNarrative__content">
            <div class="footerNarrative__content__info">
                <div class="footerNarrative__content__info__left">
                    <div class="footerNarrative__content__info__left__text">
                        <p>
                            Straying from fancy design terminology and concealed complexities,
                            our template is a testament to simplicity. From the inception to
                            the completion of your web project, we aim to provide a seamless
                            and straightforward experience.
                        </p>
                    </div>
                    <div class="footerNarrative__content__info__left__email">
                        <p>info@something.com</p>
                        <div class="footerNarrative__content__info__left__email__trait"></div>
                    </div>
                </div>
                <div class="footerNarrative__content__info__right">
                    <div class="footerNarrative__content__info__right__item">
                        <div class="footerNarrative__content__info__right__item__title">
                            <p>agency</p>
                        </div>
                        <div class="footerNarrative__content__info__right__item__content">
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="about us" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="our team" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="works" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="contact" customClass="footerAnimSubtitle" />
                            </div>
                        </div>
                    </div>
                    <div class="footerNarrative__content__info__right__item">
                        <div class="footerNarrative__content__info__right__item__title">
                            <p>social</p>
                        </div>
                        <div class="footerNarrative__content__info__right__item__content">
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="awwwards" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="dribbble" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="instagram" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="savee" customClass="footerAnimSubtitle" />
                            </div>
                        </div>
                    </div>
                    <div class="footerNarrative__content__info__right__item">
                        <div class="footerNarrative__content__info__right__item__title">
                            <p>single page</p>
                        </div>
                        <div class="footerNarrative__content__info__right__item__content">
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="privacy and policy" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="credits" customClass="footerAnimSubtitle" />
                            </div>
                            <div class="footerNarrative__content__info__right__item__content__item">
                                <AnimSubtitle text="support" customClass="footerAnimSubtitle" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="footerNarrative__content__title">
                <div class="footerNarrative__content__title__box">
                    <div class="footerNarrative__content__title__box__carrousel">STUDIO NARRATIVE</div>
                    <div class="footerNarrative__content__title__box__carrousel" aria-hidden="true">STUDIO NARRATIVE</div>
                    <div class="footerNarrative__content__title__box__carrousel" aria-hidden="true">STUDIO NARRATIVE</div>
                </div>
            </div>
            <div class="footerNarrative__content__credits">
                <div class="footerNarrative__content__credits__left">
                    <div>
                        <p>© 2024 NARRATIVE.</p>
                    </div>
                    <div>
                        <p>Design works by <a>Kaixin Soymilk</a></p>
                    </div>
                </div>
                <div class="footerNarrative__content__credits__right">
                    <div class="footerNarrative__content__credits__right__point"></div>
                    <div>
                        <p>Tashkent, GMT 5+ 12:30</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { gsap } from "gsap";
import AnimSubtitle from "./AnimSubtitle.vue";
export default {
    name: "FooterNarrative",
    components: {
        AnimSubtitle,
    },
    data() {
    return {
      carrouselWidth: null,
    };
  },
    mounted() {
        this.startCarouselFooter();
    },
    methods: {
        startCarouselFooter() {
            const carrouselWidth = document.querySelector(".footerNarrative__content__title__box__carrousel").offsetWidth;
            // const titleWidth = document.querySelector(".footerNarrative__content__title").offsetWidth;
            gsap.set(".footerNarrative__content__title__box__carrousel", {
                x: (i) => -i * (carrouselWidth + 30),
                right: -carrouselWidth,
            });
            gsap.to(".footerNarrative__content__title__box__carrousel", {
                duration: 10,
                ease: "none",
                x: `-=` + ((carrouselWidth * 3) + 90), // Change this line to move in the opposite direction
                modifiers: {
                    x: gsap.utils.unitize(x => parseFloat(x) % ((carrouselWidth * 3) + 90)),
                },
                repeat: -1
            });
        },
    }
};
</script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.footerNarrative {
    display: flex;
    height: min-content;
    overflow: hidden;
    padding: 80px 32px 120px;
    position: relative;
    background-color: $dark;

    &__content {
        display: flex;
        flex-direction: column;
        height: min-content;
        overflow: visible;
        position: relative;
        width: 100%;

        &__info {
            display: flex;
            gap: 32px;
            justify-content: space-between;
            position: relative;
            width: 100%;

            &__left {
                display: flex;
                flex-direction: column;
                gap: 32px;
                height: min-content;
                position: relative;
                width: min-content;
                color: $light;
                font-family: $inter;
                text-transform: uppercase;

                &__text {
                    width: 346px;
                    word-break: break-word;
                    word-wrap: break-word;

                    p {
                        font-size: 14px;
                        letter-spacing: -0.02em;
                        font-weight: 500;
                    }
                }

                &__email {
                    cursor: pointer;
                    display: flex;
                    flex-direction: column;
                    gap: 4px;
                    height: min-content;
                    position: relative;
                    text-decoration: none;
                    width: min-content;

                    p {
                        font-size: 16px;
                        letter-spacing: -0.02em;
                        font-weight: 500;
                    }

                    &__trait {
                        align-self: stretch;
                        flex: none;
                        height: 2px;
                        overflow: hidden;
                        position: relative;
                        width: auto;
                        background-color: $light;
                    }
                }
            }

            &__right {
                display: flex;
                gap: 80px;
                height: min-content;
                position: relative;
                width: min-content;
                color: $light;
                font-family: $inter;
                text-transform: uppercase;
                font-size: 12px;

                &__item {
                    display: flex;
                    flex-direction: column;
                    gap: 16px;
                    height: min-content;
                    position: relative;
                    width: min-content;
                    white-space: pre;

                    &__title {
                        opacity: 0.5;
                        font-size: 12px;
                        letter-spacing: -0.02em;
                        font-weight: 500;
                    }

                    &__content {
                        display: flex;
                        flex-direction: column;
                        gap: 12px;
                        height: min-content;
                        position: relative;
                        width: min-content;

                        &__item {
                            cursor: pointer;
                            display: flex;
                            height: 22px;
                            position: relative;
                            text-decoration: none;
                            width: min-content;
                        }
                    }
                }
            }
        }

        &__title {
            position: relative;
            // width: 100%;
            height: 203px;
            overflow: hidden;
            transform: none;
            &__box {
                padding: 10px 0;
                position: relative;
                box-sizing: border-box;
                display: flex;transform: none;
                &__carrousel {
                    transform: none;
                    display: flex;
                    position: absolute;
                    font-size: 145px;
                    font-weight: 700;
                    line-height: 1.4em;
                    font-family: $inter;
                    color: $light;
                }
            }
        }

        &__credits {
            display: flex;
            height: min-content;
            justify-content: space-between;
            position: relative;
            width: 100%;
            font-family: $inter;
            text-transform: uppercase;
            font-size: 14px;
            letter-spacing: -0.02em;
            font-weight: 500;
            color: $light;

            &__left {
                display: flex;
                gap: 32px;
                height: min-content;
                position: relative;

                a:hover {
                    text-decoration: underline;
                }
            }

            &__right {
                align-items: center;
                display: flex;
                gap: 8px;
                height: min-content;
                position: relative;
                width: min-content;
                white-space: pre;

                &__point {
                    height: 4px;
                    position: relative;
                    width: 4px;
                    background-color: $light;
                    border-radius: 100%;
                }
            }
        }
    }
}

.footerAnimSubtitle {
    color: $light;
}
</style>
