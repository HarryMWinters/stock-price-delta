<template>
  <div class="StockPicker">
    <table>
      <thead>
        <tr>
          <th>Ticker Symbol</th>
          <th>Initial Share Price</th>
          <th>Final Share Price</th>
        </tr>
      </thead>
      <tr v-bind:key="stock.name" v-for="stock in stocks">
        <td>{{stock.symbol}}</td>
        <td v-if="stock.errMsg" class="errorMsg">Unable to retrieve data.</td>
        <td v-if="!stock.errMsg">$ {{stock.initialSharePrice}}</td>
        <td v-if="!stock.errMsg">$ {{stock.finalSharePrice}}</td>
        <td v-on:click="deleteStock(stock)" id="deleteButton">x</td>
      </tr>
    </table>
    <div id="newStock">
      <button v-on:click="submitStock">
        <img src="@/assets/add.png" />
      </button>
      <input
        type="text"
        id="stockInputField"
        value="Search ticker symbol."
        v-on:focus="clearInput"
        v-on:keydown.enter="submitStock"
      />
    </div>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  name: "StockPicker",
  props: {
    stocks: Array,
    dates: Object
  },
  methods: {
    clearInput: function(event) {
      if (event.srcElement.value == event.srcElement.defaultValue) {
        event.srcElement.value = "";
      }
    },
    submitStock: function() {
      const symbol = document
        .getElementById("stockInputField")
        .value.toUpperCase();
      document.getElementById("stockInputField").value =
        symbol == "SEARCH TICKER SYMBOL." ? "Search ticker symbol" : symbol;
      const apikey = "9TYZNYNMGKH18KZ7";

      if (
        symbol &&
        symbol != "SEARCH TICKER SYMBOL." &&
        this.stocks.map(s => s.symbol).indexOf(symbol) == -1
      ) {
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
              return Number(
                response.data["Time Series (Daily)"][date]["4. close"],
                2
              );
            });

            this.stocks.push({
              symbol: symbol,
              initialSharePrice: Number(
                response.data["Time Series (Daily)"][this.dates.initial][
                  "1. open"
                ]
              ).toFixed(2),
              finalSharePrice: Number(
                response.data["Time Series (Daily)"][this.dates.final][
                  "4. close"
                ]
              ).toFixed(2),
              priceArray: stockPrices
            });
          })
          .catch(() => {
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
          });
      }
    },

    deleteStock: function(targetStock) {
      const index = this.stocks.map(s => s.symbol).indexOf(targetStock.symbol);
      this.stocks.splice(index, 1);
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.StockPicker {
  background: var(--bg-element);
  border: 1px var(--border) solid;
  margin: 1rem;
  padding: 0;
  height: 22em;
}

table {
  width: 90%;
  border-collapse: collapse;
  border-bottom: 1px solid #454545;
  margin: 5%;
}

thead {
  border-bottom: 1px solid #454545;
  font-weight: bolder;
  width: 100%;
}

th {
  padding: 0.2rem 0.5rem;
}

td {
  text-align: center;
  padding: 0.5em;
  border-bottom: 1px solid #454545;
}

img {
  height: 2em;
  width: 2em;
}

button {
  padding: 1em;
  border: none;
  cursor: pointer;
  outline: none;
  border: 1px var(--border) solid;
  margin-left: 1em;
}

button:active {
  background: #656565;
}

input {
  font-size: 1.5em;
  margin: 0rem;
  margin-left: 0.5rem;
  font-weight: 600;
  padding-left: 0.5em;
}

#newStock {
  margin: 1em;
  display: flex;
  flex-direction: row;
  width: 60%;
}

.errorMsg {
  color: red;
  font-weight: 900;
}

#deleteButton {
  color: red;
  font-weight: 900;
  margin: 1em;
  height: 1em;
  padding: 4px;
}

#deleteButton:hover {
  cursor: pointer;
}
</style>
