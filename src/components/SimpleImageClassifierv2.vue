<template>
  <div>
    <input type="file" accept="image/*" @change="classifyImage" />
    <img v-if="imageUrl" :src="imageUrl" alt="Uploaded Image" style="max-width: 300px;" />
    <p v-if="result">{{ result }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      imageUrl: null,
      result: null,
    };
  },
  methods: {
    async classifyImage(event) {
      const file = event.target.files[0];
      if (!file) return;

      const reader = new FileReader();
      reader.readAsDataURL(file);

      reader.onload = async (e) => {
        this.imageUrl = e.target.result;

        // Use Teachable Machine endpoint for classification
        const modelEndpoint = 'https://storage.googleapis.com/tm-model/mN5Nmh2wD/model.json';
        const formData = new FormData();
        formData.append('image', file);

        try {
          const response = await axios.post(modelEndpoint, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          });

          // Assuming response.data contains the predictions
          const predictions = response.data;

          // Update result based on the predictions
          // You might need to customize this based on the structure of Teachable Machine's response
          const result = predictions[0].className;
          this.result = result;
        } catch (error) {
          console.error('Error classifying image:', error);
        }
      };
    },
  },
};
</script>
