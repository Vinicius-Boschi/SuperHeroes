<template>  
  <Heroes />
</template>

<script>
  import Heroes from './components/Heroes.vue'

  export default {
    name: 'App',
    components: {
      Heroes
    }
  }
</script>

<style lang="scss">
  @import "./assets/variable.scss";

  #app {
    font-family: $font;
  }
</style>