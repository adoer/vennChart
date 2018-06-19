<template>
  <div id="app">
    <container/>
  </div>
</template>

<script>
import container from './components/container'
export default {
  name: 'App',
  components: {
    container
  }
}
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
