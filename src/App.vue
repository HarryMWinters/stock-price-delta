<template>
  <div id="app">
    <Nav />
    <ValueGraph class="large" />
    <ControlPanel v-bind:stocks="stocks" v-bind:dates="dates" />
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
  },
  data() {
    return {
      stocks: [],

      dates: {
        initial: "2019-07-01",
        final: "2019-07-02"
      }
    };
  }
};
</script>

<style>
* {
  --black: #020202;
  --eggshell: #f1f7ed;
  --lime: #8edce6;
  --grey: #454545;
  --forest: #4f9d69;

  margin: 0;
  padding: 0;
}

body {
  height: 100%;
  background: var(--eggshell);
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
