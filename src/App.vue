<template>
  <div id="app">
    <img
      alt="Vue logo"
      src="./assets/logo.png"
    />
    <People msg="Welcome to Your Vue.js App" />
    <Connection msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
  import Vue from 'vue'
  import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

  Vue.use(BootstrapVue)
  Vue.use(IconsPlugin)

  import Connection from './components/Connection.vue'

  import People from './components/People.vue'

  export default {
    name: 'App',
    components: {
      People,
      Connection
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
    margin-top: 60px;
  }
</style>
