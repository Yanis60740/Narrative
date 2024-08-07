<template>
  <NavBar/>
  <HeroBanner/>
</template>

<script>
import NavBar from './components/NavBar.vue'
import HeroBanner from './components/HeroBanner.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    HeroBanner
  }
}
</script>

<style lang="scss" >
@import "css/global.scss";
</style>
