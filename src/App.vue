<template>
  <div id="app">
    <Vega :mode="mode" />

    <input type="radio" id="low" value="low" v-model="mode">
    <label for="selection">Low</label>
    <br>
    <input type="radio" id="high" value="high" v-model="mode">
    <label for="time">High</label>
  </div>
</template>

<script>
import Vega from './components/Vega.vue'

export default {
  name: 'app',
  components: {
    Vega
  },
  data () {
    return {
      mode: 'low'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
