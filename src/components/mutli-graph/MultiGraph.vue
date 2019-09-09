<template>
  <div>
    <div v-if="chart.series[0] != undefined">
      <v-chart :options="chart" autoresize />
    </div>
    <div id="initialMessageBoard" v-else>
      <h3>Enter a ticker symbol below to generate a graph.</h3>
    </div>
  </div>
</template>

<script>
import ECharts from "vue-echarts";
import "echarts";

export default {
  name: "MultiGraph",
  components: {
    "v-chart": ECharts
  },
  props: { chart: Object }
};
</script>

<style scoped>
.echarts {
  padding: 0.2em;
  width: 100%;
  margin: 0rem;
  height: 17em;
}

#initialMessageBoard {
  padding: 1em;
  width: 100%;
  margin: 0rem;
  height: 16em;
}
</style>
