<template>
  <canvas
    v-bind:width="width"
    v-bind:height="height"
    v-bind:style="canvasStyle"
    v-on:mousedown.prevent="startPoint"
    v-on:mousemove.prevent="movePoint"
    v-on:mouseup.prevent="endPoint"
    v-on:touchstart.prevent="startPoint"
    v-on:touchmove.prevent="movePoint"
    v-on:touchend.prevent="endPoint"
  ></canvas>
</template>

<script>
export default {
  name: "DrawingCanvas",
  props: {
    width: {
      type: String,
      default: 100
    },
    height: {
      type: String,
      default: 100
    },
    canvasStyle: {
      type: String
    },
    penSize: {
      type: Number,
      default: 14
    },
    penColor: {
      type: String,
      default: "white"
    },
    backgroundColor: {
      type: String,
      default: "black"
    }
  },
  methods: {
    startPoint(e) {
      this.ctx.beginPath();
      this.X = e.layerX;
      this.Y = e.layerY;
      this.ctx.moveTo(this.X, this.Y);
    },
    movePoint(e) {
      if (e.buttons === 1 || e.witch === 1 || e.type == "touchmove") {
        this.X = e.layerX;
        this.Y = e.layerY;
        this.moveflg = true;
        this.ctx.lineTo(this.X, this.Y);
        this.ctx.lineWidth = this.penSize;
        this.ctx.strokeStyle = this.penColor;
        this.ctx.stroke();
      }
    },
    endPoint(e) {
      if (this.moveflg === false) {
        this.ctx.lineTo(this.X - 1, this.Y - 1);
        this.ctx.lineWidth = this.penSize;
        this.ctx.strokeStyle = this.penColor;
        this.ctx.stroke();
      }
      this.moveflg = false;
    },
    clear() {
      this.ctx.clearRect(
        0,
        0,
        this.ctx.canvas.clientWidth,
        this.ctx.canvas.clientHeight
      );
      this.ctx.fillStyle = this.backgroundColor;
      this.ctx.fillRect(
        0,
        0,
        this.ctx.canvas.clientWidth,
        this.ctx.canvas.clientWidth
      );
    },
    getImageData(width = 28, height = 28) {
      this.ctx.drawImage(this.canvas, 0, 0, width, height);
      return this.canvas.getImageData(0, 0, width, height);
    }
  },
  mounted() {
    this.canvas = this.$el;
    this.ctx = this.canvas.getContext("2d");
    this.ctx.lineCap = "round";
    this.clear();
  }
};
</script>

<style scoped>
</style>
