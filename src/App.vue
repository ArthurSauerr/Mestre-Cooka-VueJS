<template>
    <div id="app">
    <Navbar />
    <router-view />
  </div>

  <MestreCooka/>
</template>

<script>
import MestreCooka from './components/MestreCooka.vue'
import Navbar from './components/Navbar.vue';

export default {
  name: 'App',
  components: {
    MestreCooka,
    Navbar
  }
}
</script>

<style>
body{
  background-color: #EBE2DE;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #130c00;
  margin-top: 40px;
}
</style>
