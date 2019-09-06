<template>
  <div class="ControlPanel">
    <StockPicker />
    <div class="col">
      <ValueGraph />
      <ValueReadout />
    </div>
  </div>
</template>

<script>
import StockPicker from "../stock-picker/StockPicker.vue";
import ValueGraph from "../value-graph/ValueGraph.vue";
import ValueReadout from "./value-readout/ValueReadout.vue";

export default {
  name: "ControlPanel",
  props: {
    msg: String
  },
  components: {
    StockPicker,
    ValueGraph
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