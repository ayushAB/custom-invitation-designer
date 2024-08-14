<template>
    <div class="p-4 space-y-4 bg-white shadow-md rounded-lg">
      <div>
        <input type="file" @change="handleImageUpload" />
      </div>
      <div>
        <button @click="addShape" class="px-4 py-2 bg-blue-500 text-white rounded">Add Shape</button>
      </div>
      <div>
        <input v-model="text" type="text" placeholder="Enter text" class="px-4 py-2 border rounded" />
        <button @click="addText" class="px-4 py-2 bg-green-500 text-white rounded">Add Text</button>
      </div>
      <div>
        <button @click="downloadCanvas" class="px-4 py-2 bg-red-500 text-white rounded">Download Invitation</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        text: '',
      };
    },
    methods: {
      handleImageUpload(event) {
        const file = event.target.files[0];
        if (file) {
          this.$emit('image-upload', file);
        }
      },
      addShape() {
        this.$emit('add-shape');
      },
      addText() {
        this.$emit('add-text', this.text);
      },
      downloadCanvas() {
        this.$emit('download-canvas');
      },
    },
  };
  </script>
  