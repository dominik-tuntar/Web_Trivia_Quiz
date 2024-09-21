<template>
  <div id="app">
    <mainFrame></mainFrame>
    <gameFrame></gameFrame>
  </div>
</template>

<script>
import mainFrame from './components/mainFrame.vue'
import gameFrame from './components/gameFrame.vue'
export default {
  name: 'App',
  components: {
    mainFrame,
    gameFrame
  }
}
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
