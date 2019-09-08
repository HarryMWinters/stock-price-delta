<template>
  <div id="app">
    <Nav />
    <MultiGraph />
    <ControlPanel v-bind:stocks="stocks" v-bind:dates="dates" />
  </div>
</template>

<script>
import Nav from "./components/nav//Nav.vue";
import ControlPanel from "./components/control-panel/ControlPanel.vue";
import MultiGraph from "./components/mutli-graph/MultiGraph.vue";

export default {
  name: "app",
  components: {
    Nav,
    MultiGraph,
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
  --eggshell: #ffffff;
  --lime: #8edce6;
  --grey: #454545;
  --forest: #4f9d69;

  --bg-element: #ffffff;
  --border: #45454538;

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
