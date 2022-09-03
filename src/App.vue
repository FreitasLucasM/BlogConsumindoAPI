<template>
  <div id="app">
    <navbarVue/>
    <artigosVue></artigosVue>
  </div>
</template>
<script>
import artigosVue from './components/artigosVue.vue'
import navbarVue from './components/navbar.vue';

export default {
  name: 'App',
  components: {
    artigosVue,
    navbarVue
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
}
*{
    margin: 0;
    padding: 0;
  }
</style>
