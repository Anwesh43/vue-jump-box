<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <JumpBox/>
</template>

<script>
import JumpBox from './components/JumpBox'
export default {
  name: 'App',
  components: {
    JumpBox
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
