<template>
  <div id="app">
    <nav-bar />
    <login-modal v-if="!loggedIn" />
    <board />
  </div>
</template>

<script>
import Board from '@/views/Board'
import NavBar from '@/NavBar'
import LoginModal from '@/views/LoginModal'
import _isEmpty from 'lodash/isEmpty'

export default {
  name: 'app',
  components: {
    Board,
    NavBar,
    LoginModal
  },
  data() {
    return {
      user: {}
    }
  },
  computed: {
    loggedIn() {
      return !_isEmpty(this.user)
    }
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
