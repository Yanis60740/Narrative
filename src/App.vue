<template>
  <NavBar/>
  <Title/>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Title from './components/Title.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    Title
  }
}
</script>

<style lang="scss" >
@import "css/global.scss";
</style>
