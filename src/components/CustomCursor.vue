<template>
  <div class="custom-cursor-container">
    <div ref="customCursor" class="custom-cursor" :class="{ active: isActive }">
      <span class="cursor-text">{{ cursorText }}</span>
    </div>
  </div>
</template>

<script>
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
      
      // Ajuster la position pour centrer le curseur sur la souris
      cursor.style.left = `${event.clientX - cursorWidth / 2}px`;
      cursor.style.top = `${event.clientY - cursorHeight / 2}px`;
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
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background-color: rgb(0 0 0 / 20%);
  backdrop-filter: blur(5px);
  display: flex;
  justify-content: center;
  align-items: center;
  pointer-events: none;
  transition: transform 0.2s ease-in-out, background-color 0.2s ease-in-out;
  opacity: 0;
  visibility: hidden;
}
.custom-cursor.active {
  opacity: 1;
  visibility: visible;  /* Lorsque la classe active est appliquée, le curseur devient visible */
}

.cursor-text {
  font-size: 12px;
  color: rgb(255, 255, 255);
  pointer-events: none; /* Prevent text from interfering with events */
}
.video:hover ~ .custom-cursor {
  transform: scale(1.5); /* Enlarge the cursor when hovering over the video */
  background-color: rgba(255, 255, 255, 0.9);
}
</style>
