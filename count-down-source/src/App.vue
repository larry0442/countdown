<template>
  <div id="app">
    <HomePage />
  </div>
</template>

<script>
import HomePage from './components/HonePage'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style>
#app {
  width:100%;
  height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
