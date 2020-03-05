<template>
  <div id="app">
    <p><a href="https://github.com/brunohenriquy/vue-yes-no">GitHub Repo</a></p>
    <img alt="Vue logo" src="./assets/logo.png">
    <YesNo/>
  </div>
</template>

<script>
  import YesNo from './components/YesNo.vue'

  export default {
    name: 'App',
    components: {
      YesNo
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
