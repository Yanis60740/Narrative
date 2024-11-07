<template>
  <div class="custom-cursor-container">
    <div ref="customCursor" class="custom-cursor" :class="{ active: isActive }">
      <span class="cursor-text">{{ cursorText }}</span>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
export default {
  name: "CustomCursor",
  data() {
    return {
      cursorText: "",
      isActive: false,
    };
  },
  mounted() {
    document.addEventListener("mousemove", this.moveCursor);
  },
  beforeUnmount() {
    // Remove event listener to avoid memory leaks
    document.removeEventListener("mousemove", this.moveCursor);
  },
  methods: {
    moveCursor(event) {
      const cursor = this.$refs.customCursor;

      const cursorWidth = cursor.offsetWidth;
      const cursorHeight = cursor.offsetHeight;

      gsap.to(cursor, {
        duration: 0.8,
        x: event.clientX - cursorWidth / 2,
        y: event.clientY - cursorHeight / 2,
        ease: "power3.out",
      });
    },
    setCursorText(text) {
      this.cursorText = text; // Change cursor text when hovering over elements
      this.isActive = true;
    },
    resetCursorText() {
      this.cursorText = ""; // Reset cursor text when leaving elements
      this.isActive = false;
    },
  },
};
</script>
<!-- autoAlpha à la place de opacity // willchange -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "../css/global.scss";
.custom-cursor-container {
  cursor: none;
}

/* Custom cursor styles */
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background-color: rgb(0 0 0 / 20%);
  backdrop-filter: blur(5px);
  display: flex;
  justify-content: center;
  align-items: center;
  pointer-events: none;
  opacity: 0;
  visibility: hidden;
}
.custom-cursor.active {
  opacity: 1;
  visibility: visible; /* Lorsque la classe active est appliquée, le curseur devient visible */
}

.cursor-text {
  font-size: 12px;
  color: rgb(255, 255, 255);
  pointer-events: none; /* Prevent text from interfering with events */
}
</style>
