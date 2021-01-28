<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <User />
  </div>
</template>

<script>
import User from './components/User.vue'

export default {
  name: 'App',
  components: {
    User
  }
}
</script>

<style lang="scss">
@import "styles/main.scss";

/* #app {

} */
</style>
 