<template>
    <div>
      <h2>Upload a PDF File</h2>
      <input type="file" @change="handleFileChange" />
      <button @click="uploadFile">Upload</button>
      <p v-if="message">{{ message }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectedFile: null,
        message: ''
      };
    },
    methods: {
      handleFileChange(event) {
        this.selectedFile = event.target.files[0];
      },
      async uploadFile() {
        if (!this.selectedFile) {
          this.message = 'Please select a file first';
          return;
        }
  
        const formData = new FormData();
        formData.append('file', this.selectedFile);
  
        try {
          const response = await fetch('http://localhost:3000/upload', {
            method: 'POST',
            body: formData
          });
          const result = await response.json();
          this.message = result.message;
        } catch (error) {
          console.error('Error uploading file:', error);
          this.message = 'File upload failed';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  button {
    margin-top: 10px;
  }
  </style>
   
