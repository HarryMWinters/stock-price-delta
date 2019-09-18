<template>
  <div id="app">
    <Nav v-bind:toggleIntro="toggleIntro" />
    <article v-if="showIntro" class="message is-dark">
      <div class="message-header">
        <p id="introText">About this App</p>
        <button class="delete" aria-label="delete" @click="toggleIntro"></button>
      </div>
      <div class="message-body">
        <p>
          <strong>Hey! Thanks for visiting this site.</strong> I made this app after a certain
          <a
            href="https://www.google.com/search?q=guideline+financial"
          >unnamed</a> financial institution was taking months to disburse my 401k and I got curious about how my portfolio would have behaved in the interim.
          Poorly it turns out but now the world got a web app out of it so...winning?
        </p>
        <br />
        <p>
          Anyways, if you're here you probably wanna play with it. Choose the date range you're interested in where it says
          <strong>"Select a date range.."</strong>and search for stocks by ticker symbol. I.E. TSLA for Tesla Motors or GOOG
          for Google. Don't worry if you enter an unknown symbol. It'll let you know and you can delete and re-enter it.
        </p>
        <br />
        <p>
          Finally, there's a lot more I'd like to do with this app (but I probably won't). Check out the
          <a
            href="https://github.com/HarryMWinters/stock-price-delta"
            rel="noopener noreferrer"
            target="_blank"
          >Github</a> link if your curious about what I would put in the next version.
        </p>
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
      // ToDo: Update element in place rather then poping it out and repushing it.
      this.stocks.push({
        symbol: symbol,
        isLoading: true
      });
      const today = new Date();
      const threeMonthsAgo = new Date(
        today.getFullYear(),
        today.getMonth() - 3,
        today.getDate()
      );
      const initialDate = new Date(
        this.dates.initial.slice(0, 4),
        this.dates.initial.slice(5, 7),
        this.dates.initial.slice(8, 10)
      );

      const outputsize = initialDate > threeMonthsAgo ? "compact" : "full";

      axios
        .get("https://www.alphavantage.co/query", {
          params: {
            function: "TIME_SERIES_DAILY",
            symbol: symbol,
            apikey: apikey,
            outputsize: outputsize
          }
        })
        .then(response => {
          this.stocks.pop();
          if (response.data["Error Message"]) {
            this.stocks.push({
              symbol: symbol,
              initialSharePrice: null,
              finalSharePrice: null,
              errMsg:
                "Unable to retrieve data for " +
                symbol +
                ". Please check that the symbol is listed on the NASDAQ, AMEX or NYSE."
            });
          } else {
            const dates = Object.keys(response.data["Time Series (Daily)"]);
            let stockPrices = dates.map(date => {
              return [
                Number(
                  response.data["Time Series (Daily)"][date]["4. close"],
                  2
                ),
                date
              ];
            });

            let loopCounter = 0;
            while (!response.data["Time Series (Daily)"][this.dates.initial]) {
              // Choose next date market is open.
              loopCounter++;
              if (loopCounter > 10) {
                throw "Too many loop iterations attempting to find initial market open date.";
              }
              this.dates.initial = new Date(
                this.dates.initial.slice(0, 4),
                this.dates.initial.slice(5, 7),
                Number(this.dates.initial.slice(8, 10)) + 1
              )
                .toISOString()
                .slice(0, 10);
            }
            loopCounter = 0;
            if (!response.data["Time Series (Daily)"][this.dates.final]) {
              loopCounter++;
              if (loopCounter > 10) {
                throw "Too many loop iterations attempting to find final market open date.";
              }
              this.dates.initial = new Date(
                this.dates.final.slice(0, 4),
                this.dates.final.slice(5, 7),
                Number(this.dates.final.slice(8, 10)) + 1
              )
                .toISOString()
                .slice(0, 10);
            }
            this.stocks.push({
              symbol: symbol,
              isLoading: false,
              initialSharePrice: Number(
                response.data["Time Series (Daily)"][this.dates.initial][
                  "4. close"
                ]
              ).toFixed(2),
              finalSharePrice: Number(
                response.data["Time Series (Daily)"][this.dates.final][
                  "4. close"
                ]
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
              data: Object.keys(response.data["Time Series (Daily)"]).map(
                day => {
                  if (
                    new Date(day) >= new Date(this.dates.initial) &&
                    new Date(day) <= new Date(this.dates.final)
                  ) {
                    return [
                      day,
                      response.data["Time Series (Daily)"][day]["4. close"]
                    ];
                  }
                }
              )
            });
            this.showIntro = false;
          }
        })
        .catch(err => {
          this.stocks.pop();
          this.stocks.push({
            symbol: symbol,
            initialSharePrice: null,
            finalSharePrice: null,
            errMsg:
              "Unable to retrieve data for " +
              symbol +
              " in range " +
              this.dates.initial +
              " to " +
              this.dates.final +
              "."
          });
          throw err;
        });
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
      if (this.stocks.length != 0) {
        // Warn user that changing the date will erase their stocks.
        // ToDo: Give the user the option to simply refresh all their stocks.
        if (
          confirm(
            "Changing the date range will erase all loaded stock data. Continue?"
          )
        ) {
          this.stocks = [];
          this.stackedChart.series = [];
          this.stackedChart.legend.data = [];
          this.dates.initial = date.toISOString().slice(0, 10);
        }
      } else {
        this.dates.initial = date.toISOString().slice(0, 10);
      }
    },
    finalDateUpdater: function(date) {
      if (this.stocks.length != 0) {
        // Warn user that changing the date will erase their stocks.
        // ToDo: Give the user the option to simply refresh all their stocks.
        if (
          confirm(
            "Changing the date range will erase all loaded stock data. Continue?"
          )
        ) {
          this.stocks = [];
          this.stackedChart.series = [];
          this.stackedChart.legend.data = [];
          this.dates.final = date.toISOString().slice(0, 10);
        }
      } else {
        this.dates.final = date.toISOString().slice(0, 10);
      }
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
  --bg-element: #ffffff;
  --border: #45454538;

  margin: 0;
  padding: 0;
}

body {
  height: 100%;
  background: var(--eggshell);
  min-width: 748px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
article {
  height: 18em;
}
p {
  padding: 1em;
}
</style>
