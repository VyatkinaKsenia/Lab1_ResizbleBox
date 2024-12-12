<template>
  <div>
    <div class="resizable-box"
         @mousedown="startResize1"
         :style="boxStyle1">
      <div class="resize-handle" @mousedown.stop="startResize1"></div>
      <p>Окно №1</p>
    </div>

    <div class="resizable-box"
         @mousedown="startResize2"
         :style="boxStyle2">
      <div class="resize-handle" @mousedown.stop="startResize2"></div>
      <p>Окно №2</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      width1: 200,
      height1: 150,
      isResizing1: false,
      initialX1: 0,
      initialY1: 0,
      initialWidth1: 0,
      initialHeight1: 0,

      width2: 100,
      height2: 100,
      isResizing2: false,
      initialX2: 0,
      initialY2: 0,
      initialWidth2: 0,
      initialHeight2: 0,
    };
  },

  methods: {
    startResize1(event) {
      this.isResizing1 = true;
      this.initialX1 = event.clientX;
      this.initialY1 = event.clientY;
      this.initialWidth1 = this.width1;
      this.initialHeight1 = this.height1;

      document.addEventListener('mousemove', this.resize1);
      document.addEventListener('mouseup', this.stopResize1);
    },
    resize1(event) {
      if (!this.isResizing1) return;
      const deltaX = event.clientX - this.initialX1;
      const deltaY = event.clientY - this.initialY1;
      this.width1 = Math.max(100, this.initialWidth1 + deltaX); // Минимальная ширина 100px
      this.height1 = Math.max(50, this.initialHeight1 + deltaY); // Минимальная высота 50px
    },
    stopResize1() {
      this.isResizing1 = false;
      document.removeEventListener('mousemove', this.resize1);
      document.removeEventListener('mouseup', this.stopResize1);
    },

    startResize2(event) {
      this.isResizing2 = true;
      this.initialX2 = event.clientX;
      this.initialY2 = event.clientY;
      this.initialWidth2 = this.width2;
      this.initialHeight2 = this.height2;

      document.addEventListener('mousemove', this.resize2);
      document.addEventListener('mouseup', this.stopResize2);
    },
    resize2(event) {
      if (!this.isResizing2) return;
      const deltaX = event.clientX - this.initialX2;
      const deltaY = event.clientY - this.initialY2;
      this.width2 = Math.max(100, this.initialWidth2 + deltaX); // Минимальная ширина 100px
      this.height2 = Math.max(50, this.initialHeight2 + deltaY); // Минимальная высота 50px
    },
    stopResize2() {
      this.isResizing2 = false;
      document.removeEventListener('mousemove', this.resize2);
      document.removeEventListener('mouseup', this.stopResize2);
    },
  },
  computed: {
    boxStyle1() {
      return { width: this.width1 + 'px', height: this.height1 + 'px' };
    },
    boxStyle2() {
      return { width: this.width2 + 'px', height: this.height2 + 'px' };
    }
  }
};
</script>

<style scoped>
.resizable-box {
  background-color: #c3b3ff;
  border: 2px solid #000000;
  position: relative;
  cursor: nwse-resize;
  padding: 10px;
  margin-bottom: 10px; /* разделения окон */
  display: flex;
  align-items: center; /* Центрирование по вертикали */
  justify-content: center; /* Центрирование по горизонтали */
}

.resize-handle {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 10px;
  height: 10px;
  background-color: #000000;
  cursor: nwse-resize;
}
</style>
