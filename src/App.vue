<template>
  <div id="app">
    <Nav />
    <MultiGraph v-bind:chart="stackedChart" />
    <ControlPanel
      v-bind:stocks="stocks"
      v-bind:dates="dates"
      v-bind:updater="stockUpdater"
      v-bind:deleter="stockDeleter"
    />
  </div>
</template>

<script>
const axios = require("axios");

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

  methods: {
    stockUpdater: function(symbol) {
      const apikey = "9TYZNYNMGKH18KZ7";
      axios
        .get("https://www.alphavantage.co/query", {
          params: {
            function: "TIME_SERIES_DAILY",
            symbol: symbol,
            apikey: apikey
          }
        })
        .then(response => {
          const dates = Object.keys(response.data["Time Series (Daily)"]);
          let stockPrices = dates.map(date => {
            return [
              Number(response.data["Time Series (Daily)"][date]["4. close"], 2),
              date
            ];
          });
          this.stocks.push({
            symbol: symbol,
            initialSharePrice: Number(
              response.data["Time Series (Daily)"][this.dates.initial][
                "4. close"
              ]
            ).toFixed(2),
            finalSharePrice: Number(
              response.data["Time Series (Daily)"][this.dates.final]["4. close"]
            ).toFixed(2),
            priceArray: stockPrices
          });
          // Update graph info
          this.stackedChart.series.push({
            name: symbol,
            type: "line",
            stack: "none",
            areaStyle: {},
            data: Object.keys(response.data["Time Series (Daily)"]).map(day => {
              if (
                new Date(day) >= new Date(this.dates.initial) &&
                new Date(day) <= new Date(this.dates.final)
              ) {
                return [
                  day,
                  response.data["Time Series (Daily)"][day]["4. close"]
                ];
              }
            })
          });
        });
      // .catch(() => {
      //   this.stocks.push({
      //     symbol: symbol,
      //     initialSharePrice: null,
      //     finalSharePrice: null,
      //     errMsg:
      //       "Unable to retrieve data for " +
      //       symbol +
      //       " in range " +
      //       this.dates.initial +
      //       " to " +
      //       this.dates.final +
      //       "."
      //   });
      // });
    },
    stockDeleter: function(targetStock) {
      const index = this.stocks.map(s => s.symbol).indexOf(targetStock.symbol);
      this.stocks.splice(index, 1);
      this.stackedChart.series.splice(index, 1);
      this.stackedChart = Object.assign({}, this.stackedChart);
      // Have to fo this otherwise the layered histogram merges the states.
    },
    initialDateUpdater: function(date) {},
    finalDateUpdater: function(date) {}
  },
  data() {
    return {
      stocks: [],
      dates: {
        initial: "2019-06-07",
        final: "2019-06-17"
      },
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
        series: []
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
