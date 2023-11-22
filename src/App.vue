<template>
  <div id="app">
    <header>
      <h1>Image Classifier App</h1>
    </header>
    <main>
      <SimpleImageClassifierv2 />
    </main>
  </div>
</template>

<script>
import SimpleImageClassifierv2 from './components/SimpleImageClassifierv2.vue';

export default {
  components: {
    SimpleImageClassifierv2,
  },
};
</script>