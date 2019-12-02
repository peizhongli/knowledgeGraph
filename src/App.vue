<template>
  <div id="app">
    <Graph />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Graph from './components/Graph.vue'

export default {
  name: 'app',
  components: {
    Graph
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
  background-color: #f0f0f0;
}
</style>
