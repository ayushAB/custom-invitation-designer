<template>
  <div class="flex">
    <Controls
      @image-upload="handleImageUpload"
      @add-shape="addShape"
      @add-text="addText"
      @download-canvas="downloadCanvas"
    />
    <Canvas ref="canvas" />
  </div>
</template>

<script>
import Controls from './components/Controls.vue';
import Canvas from './components/Canvas.vue';

export default {
  components: {
    Controls,
    Canvas,
  },
  methods: {
    handleImageUpload(file) {
      this.$refs.canvas.handleImageUpload(file);
    },
    addShape() {
      this.$refs.canvas.addShape();
    },
    addText(text) {
      this.$refs.canvas.addText(text);
    },
    downloadCanvas() {
      this.$refs.canvas.downloadCanvas();
    },
  },
};
</script>
