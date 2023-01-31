<template>
  <div id="app">
    <img alt="Vue logo" src="https://vuejs.org/images/logo.png" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import getPixels from 'get-pixels';
import { extractColors } from 'extract-colors';

export default {
  name: 'App',
  setup() {
    const src = './logo.png';
    getPixels(src, (err, pixels) => {
      console.log(err);
      if (!err) {
        const data = [...pixels.data];
        const width = Math.round(Math.sqrt(data.length / 4));
        const height = width;

        extractColors({ data, width, height })
          .then(console.log)
          .catch(console.log);
      }
    });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
