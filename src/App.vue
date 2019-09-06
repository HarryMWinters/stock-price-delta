<template>
  <div id="app">
    <Nav />
    <ValueGraph class="large" />
    <ControlPanel />
  </div>
</template>

<script>
import Nav from "./components/nav//Nav.vue";
import ControlPanel from "./components/control-panel/ControlPanel.vue";
import ValueGraph from "./components/value-graph/ValueGraph.vue";

export default {
  name: "app",
  components: {
    Nav,
    ValueGraph,
    ControlPanel
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  height: 100%;
  background: #bcffdb;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
