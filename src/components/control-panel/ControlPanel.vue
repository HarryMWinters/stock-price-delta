<template>
  <div class="ControlPanel">
    <StockPicker
      v-bind:stocks="stocks"
      v-bind:dates="dates"
      v-bind:updater="updater"
      v-bind:deleter="deleter"
    />
    <div class="col">
      <DateSelectionBox
        v-bind:intialDateUpdater="initialDateUpdater"
        v-bind:finaldateUpdater="finalDateUpdater"
      />
      <ValueReadout />
    </div>
  </div>
</template>

<script>
import StockPicker from "../stock-picker/StockPicker.vue";
import DateSelectionBox from "./date-selection/DateSelectorBox.vue";
import ValueReadout from "./value-readout/ValueReadout.vue";

export default {
  name: "ControlPanel",
  props: {
    stocks: Array,
    dates: Object,
    updater: Function,
    deleter: Function,
    initialDateUpdater: Function,
    finalDateUpdater: Function
  },
  components: {
    StockPicker,
    ValueReadout,
    DateSelectionBox
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