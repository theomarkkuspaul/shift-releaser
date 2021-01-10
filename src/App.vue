<template>
  <div id="app">
    <Kraken/>
  </div>
</template>

<script>
import Kraken from './components/Kraken.vue'

export default {
  name: 'App',
  components: {
    Kraken
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
