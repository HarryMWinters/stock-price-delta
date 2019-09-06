<template>
  <div id="app">
    <Nav />
    <ValueGraph class="large" />
    <ControlPanel v-bind:stocks="stocks" />
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
      stocks: [
        { symbol: "VSATX", initialSharePrice: 1, finalSharePrice: 2 },
        { symbol: "VMATX", initialSharePrice: 1, finalSharePrice: 2 },
        { symbol: "VWESX", initialSharePrice: 1, finalSharePrice: 2 }
      ],
      initialDate: "2019-03-01",
      finaldate: "2019-07-02"
    };
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
  background: #4f9d69;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
