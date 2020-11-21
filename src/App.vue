<template>
  <div id="app">
    <simonTheGame></simonTheGame>
  </div>
</template>

<script>
import simonTheGame from './components/simonTheGame'

export default {
  name: 'App',
  components: {
    simonTheGame
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');
@import './src/sass/style.sass';
</style>
