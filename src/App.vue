<template>
  <div id="app">
    <FirstCalc></FirstCalc>
  </div>
</template>

<script>
import FirstCalc from './components/FirstCalc.vue'

export default {
  name: 'App',
  components: {
    FirstCalc
  }
}
</script>

<style lang="scss">
#app {
  text-align: right;
  font-size: 20px;
  line-height: 25px;
  max-width: 800px;
  margin: 0 auto;
  padding-top: 100px;
}
</style>
