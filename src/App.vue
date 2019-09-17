<template>
  <div id="app">
    <Nav v-bind:toggleIntro="toggleIntro" />
    <article v-if="showIntro" class="message is-dark">
      <div class="message-header">
        <p id="introText">About this App</p>
        <button class="delete" aria-label="delete" @click="toggleIntro"></button>
      </div>
      <div class="message-body">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit.
        <strong>Pellentesque risus mi</strong>, tempus quis placerat ut, porta nec nulla. Vestibulum rhoncus ac ex sit amet fringilla. Nullam gravida purus diam, et dictum
        <a>felis venenatis</a> efficitur. Aenean ac
        <em>eleifend lacus</em>, in mollis lectus. Donec sodales, arcu et sollicitudin porttitor, tortor urna tempor ligula, id porttitor mi magna a neque. Donec dui urna, vehicula et sem eget, facilisis sodales sem.
      </div>
    </article>
    <MultiGraph v-else v-bind:chart="stackedChart" />
    <StockPicker
      v-bind:stocks="stocks"
      v-bind:dates="dates"
      v-bind:updater="stockUpdater"
      v-bind:deleter="stockDeleter"
      v-bind:initialDateUpdater="initialDateUpdater"
      v-bind:finalDateUpdater="finalDateUpdater"
    />
  </div>
</template>

<script>
const axios = require("axios");

import Nav from "./components/nav//Nav.vue";
import MultiGraph from "./components/mutli-graph/MultiGraph.vue";
import StockPicker from "./components/stock-picker/StockPicker.vue";

export default {
  name: "app",
  components: {
    Nav,
    MultiGraph,
    StockPicker
  },

  methods: {
    toggleIntro: function() {
      this.showIntro = !this.showIntro;
    },
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
          this.stackedChart.legend.data.push(symbol);
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
          this.showIntro = false;
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
      // Remove graph data
      const index = this.stocks.map(s => s.symbol).indexOf(targetStock.symbol);
      this.stocks.splice(index, 1);
      this.stackedChart.series.splice(index, 1);
      this.stackedChart.legend.data.splice(index, 1);

      this.stackedChart = Object.assign({}, this.stackedChart);
      // Have to fo this otherwise the layered histogram merges the states.
    },
    initialDateUpdater: function(date) {
      this.dates.initial = date.toISOString().slice(0, 10);
    },
    finalDateUpdater: function(date) {
      this.dates.final = date.toISOString().slice(0, 10);
    }
  },
  data() {
    return {
      showIntro: true,
      stocks: [],
      dates: {
        initial: null,
        final: null
      },
      stackedChart: {
        legend: {
          data: []
          // ToDo: Think about where the legend should be and whether it should become scrollabe if
          // it contains many items.
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
