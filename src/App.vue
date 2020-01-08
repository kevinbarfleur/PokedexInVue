<template>
  <div id="app">
    <Pokedex />
  </div>
</template>

<script>
import Pokedex from './components/Pokedex'

export default {
  name: 'app',
  components: {
    Pokedex
  }
}
</script>



<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #424242;
  margin-top: 60px;
}
</style>