<template>
  <v-chart v-if="stocks" :options="stackedChart" autoresize />
</template>

<script>
import ECharts from "vue-echarts";
import "echarts";

export default {
  name: "MultiGraph",
  components: {
    "v-chart": ECharts
  },
  props: { stocks: Array, dates: Object },
  data() {
    return {
      stackedChart: {
        title: {
          text: "Price over time"
        },
        xAxis: [
          {
            type: "time",
            name: "Date",
            min: "dataMin",
            max: "dataMax"
          }
        ],
        yAxis: [
          {
            type: "value",
            name: "Value ($)",
            min: "0",
            max: "dataMax"
          }
        ],
        series: this.stocks.map(stock => {
          return {
            name: stock.symbol,
            type: "line",
            stack: "none",
            areaStyle: {},
            data: stock.priceArray.map(day => {
              return [day[1], day[0]];
            })
          };
        })
      }
    };
  }
};
console.log("foo");
</script>

<style scoped>
.echarts {
  padding: 0.2em;
  width: 100%;
  margin: 0rem;
  height: 17em;
}
</style>
