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
    @import url('https://fonts.googleapis.com/css?family=Yanone+Kaffeesatz:400,700&subset=cyrillic');

    body {
      font-family: 'Yanone Kaffeesatz', sans-serif;
      font-size: 130%;
    }

    input {
      font-size: 110%!important;
    }
</style>
