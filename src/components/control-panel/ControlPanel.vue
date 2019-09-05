<template>
  <div class="ControlPanel">
    <StockPicker />
    <ValueGraph type="individual small" />
  </div>
</template>

<script>
import StockPicker from "../stock-picker/StockPicker.vue";
import ValueGraph from "../value-graph/ValueGraph.vue";

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
</style>