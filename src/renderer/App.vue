<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'electron-vue-demo'
  }
</script>

<style>
  /* CSS */
  html, body {
    height: 100%;
  }
  #app {
    padding: 10px;
    height: 100%;
  }
</style>
