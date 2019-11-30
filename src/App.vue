<template>
  <div id="app">
    <nav-bar />
    <board />
  </div>
</template>

<script>
import Board from '@/views/Board'
import NavBar from '@/NavBar'

export default {
  name: 'app',
  components: {
    Board,
    NavBar
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
