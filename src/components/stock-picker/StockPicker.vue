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
        <td>{{stock.initialSharePrice}}</td>
        <td>{{stock.finalSharePrice}}</td>
        <td v-on:click="deleteStock(stock)">x</td>
      </tr>
    </table>
    <div id="newStock">
      <button v-on:click="submitStock">
        <img src="@/assets/add.png" />
      </button>
      <input type="text" id="stockInputField" value="Search ticker symbol." v-on:focus="clearInput" />
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
    submitStock: function(event) {
      const symbol = document
        .getElementById("stockInputField")
        .value.toUpperCase();
      document.getElementById("stockInputField").value = symbol;
      const apikey = "9TYZNYNMGKH18KZ7";

      if (symbol) {
        axios
          .get("https://www.alphavantage.co/query", {
            params: {
              function: "TIME_SERIES_DAILY",
              symbol: symbol,
              apikey: apikey
            }
          })
          .then(response => {
            this.stocks.push({
              symbol: symbol,
              initialSharePrice:
                response.data["Time Series (Daily)"][this.dates.initial][
                  "1. open"
                ],
              finalSharePrice:
                response.data["Time Series (Daily)"][this.dates.final][
                  "4. close"
                ]
            });
          })
          .catch(error => {
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
  background: var(--eggshell);
  border: 0.1em var(--grey) solid;
  margin: 1rem;
  padding: 0;
  height: 22em;
  border-radius: 5%;
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
  border-radius: 50%;
}
button {
  border-radius: 10%;
  padding: 1em;
  background: var(--lime);
  border: none;
  cursor: pointer;
  outline: none;
  border: 3px #454545 solid;
}

button:active {
  background: #656565;
}

input {
  background: transparent;
  font-size: 1.5em;
  margin: 0rem;
  margin-left: 0.5rem;
  font-weight: 600;
  padding-left: 0.5em;
  border: 3px solid #454545;
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
</style>
