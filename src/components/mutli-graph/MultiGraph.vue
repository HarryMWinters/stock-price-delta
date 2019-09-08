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
  props: { stocks: Array },
  data() {
    return {
      stackedChart: {
        title: {
          text: "Price over time"
        },
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            data: ["Foo", "周二", "周三", "周四", "周五", "周六", "周日"]
          }
        ],
        yAxis: [
          {
            type: "value"
          }
        ],
        series: this.stocks.map(stock => {
          return {
            name: stock.symbol,
            type: "line",
            stack: "none",
            areaStyle: {},
            data: stock.priceArray
          };
        })
      }
    };
  }
};
</script>

<style scoped>
.echarts {
  padding: 0.2em;
  width: 100%;
  margin: 0rem;
  height: 17em;
}
</style>
