<template>
  <div id="app">
    <Navbar />

    <div class="container">
      <router-view/>  
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar'

export default {
  components: {
    Navbar
  }
}
</script>

<style>
  @import '~materialize-css/dist/css/materialize.min.css';

  #app {
    background-color: #ccc;
    height: 100vh;
  }
</style>