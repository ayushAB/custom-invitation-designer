<template>
    <div class="w-full h-screen bg-gray-100 flex items-center justify-center relative">
      <canvas ref="canvas" class="w-full h-full border border-gray-300"></canvas>
    </div>
  </template>
  
  <script>
  import { fabric } from 'fabric';
  import { markRaw } from 'vue';
  
  export default {
    data() {
      return {
        canvas: null,
      };
    },
    mounted() {
      this.initFabricJS();
    },
    methods: {
      initFabricJS() {
        this.canvas = new fabric.Canvas(this.$refs.canvas, {
        height: window.innerHeight,
        width: window.innerWidth,
        backgroundColor: 'white',
        selection: true, // Ensure selection is enabled
      });
  
        this.canvas.on('object:modified', this.onObjectModified);
        // Handle resizing of the window
        window.addEventListener('resize', this.onWindowResize);
      },

      handleImageUpload(event) {
        const file = event.target.files[0];
        const reader = new FileReader();
  
        reader.onload = (e) => {
          fabric.Image.fromURL(e.target.result, (img) => {
            img.scaleToWidth(200);
            this.canvas.add(img);
            this.canvas.setActiveObject(img);
            this.canvas.renderAll();  // Ensure the canvas is updated
          });
        };
  
        reader.readAsDataURL(file);
      },
      addShape() {
        const shape = new fabric.Rect({
          left: 100,
          top: 100,
          fill: 'red',
          width: 100,
          height: 100,
          hasControls:true
        });
        this.canvas.add(markRaw(shape));
        this.canvas.setActiveObject(shape);
        this.canvas.renderAll();  // Ensure the canvas is updated
      },
      addText() {
        const text = new fabric.Textbox('Hello Fabric.js', {
          left: 100,
          top: 100,
          width: 200,
          fontSize: 30,
          hasControls: true,
          hasBorders: true,
          lockRotation: false,
          lockScalingFlip: false,
        });
  
        this.canvas.add(markRaw(text));
        this.canvas.setActiveObject(text);
        this.canvas.renderAll();  // Ensure the canvas is updated
      },
      downloadCanvas() {
        const dataURL = this.canvas.toDataURL('image/png');
        const link = document.createElement('a');
        link.href = dataURL;
        link.download = 'invitation.png';
        link.click();
      },
      onObjectModified() {
        // Optional: Handle object modifications if needed
        console.log('Object modified');
      },
      onWindowResize() {
        this.canvas.setHeight(window.innerHeight);
        this.canvas.setWidth(window.innerWidth);
        this.canvas.renderAll();
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add any additional scoped styles here if needed */
  </style>
  