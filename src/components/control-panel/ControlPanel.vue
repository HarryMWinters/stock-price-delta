<template>
  <div class="ControlPanel">
    <StockPicker
      v-bind:stocks="stocks"
      v-bind:dates="dates"
      v-bind:updater="updater"
      v-bind:deleter="deleter"
    />
    <div class="col">
      <SingleGraph />
      <ValueReadout />
    </div>
  </div>
</template>

<script>
import StockPicker from "../stock-picker/StockPicker.vue";
import SingleGraph from "./single-graph/SingleGraph.vue";
import ValueReadout from "./value-readout/ValueReadout.vue";

export default {
  name: "ControlPanel",
  props: {
    stocks: Array,
    dates: Object,
    updater: Function,
    deleter: Function
  },
  components: {
    StockPicker,
    SingleGraph,
    ValueReadout
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ControlPanel {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.col {
  display: grid;
  grid-template-rows: 1fr 1fr;
}
</style>