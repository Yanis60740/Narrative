<template>
    <div class="fixedButton">
        <div class="fixedButton__template">
            <div class="fixedButton__template__button">
                <p>Buy Template</p>
            </div>
        </div>
        <div class="fixedButton__framer">
            <div class="fixedButton__framer__button">
                <div class="fixedButton__framer__button__box">
                    <div class="fixedButton__framer__button__box__logo"></div>
                    <p>Made in Framer</p>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "FixedButton",
};
</script>

<style lang="scss" scoped>
@import "../css/variables.scss";

.fixedButton {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
    font-family: $inter;
    font-size: 12px;
    letter-spacing: -0.02em;
    font-weight: 500;

    &__template {
        width: min-content;
        white-space: pre;

        &__button {
            align-items: center;
            background-color: var(--token-9b365fbc-feb9-4db9-b725-72e62d68d7ad,
                    #121212);
            border-radius: 8px;
            bottom: 64px;
            box-shadow: 0 1px 2px #00000040;
            display: flex;
            flex: none;
            flex-direction: row;
            flex-wrap: nowrap;
            gap: 0px;
            height: 36px;
            justify-content: center;
            overflow: hidden;
            padding: 12px 16px;
            position: fixed;
            right: 20px;
            text-decoration: none;
            width: min-content;
            will-change: var(--framer-will-change-override, transform);
            z-index: 1;
            cursor: pointer;
            color: rgb(235, 235, 235);

            p {
                opacity: 0.9;
            }
        }
    }

    &__framer {
        &__button {
            height: 36px;
            overflow: hidden;
            position: relative;
            width: 142px;
            border-radius: 10px;
            background-color: rgb(235, 235, 235);
            box-shadow: rgba(0, 0, 0, 0.26) 0px 0.637473px 1.14745px -1.125px,
                rgba(0, 0, 0, 0.24) 0px 1.93094px 3.4757px -2.25px,
                rgba(0, 0, 0, 0.192) 0px 5.10423px 9.18761px -3.375px,
                rgba(0, 0, 0, 0.03) 0px 16px 28.8px -4.5px;
            cursor: pointer;
            color: black;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 600;
            &__box {
                display: flex;
                gap: 10px;
                width: min-content;
                white-space: pre;
                justify-content: center;
                &__logo {
                    background-image: url(../assets/framer.svg);
                    flex: 0 0 auto;
                    height: 16px;
                    position: relative;
                    width: 11px;
                    z-index: 2;
                }
            }
        }
    }
}
</style>
