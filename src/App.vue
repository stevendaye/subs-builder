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
  background: rgb(240, 240, 234);
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgb(39, 39, 39);
  padding: 25px;
}
</style>
