<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <CuurencyConvertor msg="Vue Currency Convertor"/>
</template>

<script>
import CuurencyConvertor from './components/CurrencyConvertor.vue'

export default {
  name: 'App',
  components: {
    CuurencyConvertor
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
