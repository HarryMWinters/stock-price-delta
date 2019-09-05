<template>
  <div id="app">
    <Nav />
    <ValueGraph type="aggregate large" />
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
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
