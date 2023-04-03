<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <copy_Component/>
</template>

<script>
import copy_Component from "./components/copy_Component.vue";
export default {
  name: 'App',
  components: {
    copy_Component
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
  margin-top: 60px;
}
</style>
