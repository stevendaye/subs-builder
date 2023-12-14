<template>
  <div id="app">
    <landing/>
  </div>
</template>

<script>
import Landing from './components/Landing.vue';

export default {
  name: 'App',
  components: {
    Landing
  }
}
</script>

<style>
body {
  background-image: linear-gradient(#f0f0ea, #d8d8d8, #009DFF);
  margin: 0;
  padding: 0;
  height: 100vh;
  overflow: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgb(39, 39, 39);
}
</style>
