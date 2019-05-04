<template>
  <div id="app">
    <DrawingCanvas
      ref="drawingCanvas"
      width="280"
      height="280"
      canvasStyle="border: 2px solid;"
      :penSize="penSize"
      :penColor="penColor"
      :backgroundColor="backgroundColor"
    />
    <div>
      ペンの太さ：
      <button v-on:click="penSize=8">8</button>
      <button v-on:click="penSize=14">14</button>
      <button v-on:click="penSize=22">22</button>
    </div>
    <div>
      ペンの色：
      <button v-on:click="penColor='white'">White</button>
      <button v-on:click="penColor='black'">Black</button>
      <button v-on:click="penColor='red'">Red</button>
      <button v-on:click="penColor='green'">Green</button>
      <button v-on:click="penColor='blue'">Blue</button>
      <button v-on:click="penColor='yellow'">Yellow</button>
    </div>
    <div>
      背景色：
      <button v-on:click="backgroundColor='black'">Black</button>
      <button v-on:click="backgroundColor='white'">White</button>
    </div>
    <div>
      <button v-on:click="clearCanvas">Clear</button>
    </div>
  </div>
</template>

<script>
import DrawingCanvas from "./components/DrawingCanvas.vue";

export default {
  name: "app",
  components: {
    DrawingCanvas
  },
  data() {
    return {
      // ペンの太さ
      penSize: 14,
      // ペンの色
      penColor: "white",
      // 背景色
      backgroundColor: "black",
    };
  },
  methods: {
    clearCanvas() {
      this.$refs.drawingCanvas.clear();
    }
  }
};
</script>
