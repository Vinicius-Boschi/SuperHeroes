<template>  
  <Heroes />
  <Footer />
</template>

<script>
  import Heroes from './components/Heroes.vue'
  import Footer from './components/Footer.vue'

  export default {
    name: 'App',
    components: {
      Heroes,
      Footer
    }
  }
</script>

<style lang="scss">
  @import "./assets/variable.scss";

  #app {
    font-family: $font;
    background-color: $black;
  }
</style>