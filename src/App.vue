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
    name: 'app',
    components: {
      Navbar
    }
  }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Dosis:400,700');

    body {
      font-family: 'Dosis', sans-serif;
      font-size: 110%;
    }
</style>
