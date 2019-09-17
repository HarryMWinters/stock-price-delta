<template>
  <div class="StockPicker">
    <table>
      <thead>
        <tr>
          <th>Ticker Symbol</th>
          <th>Initial Share Price</th>
          <th>Final Share Price</th>
          <th>Dollar Δ</th>
          <th>% Δ</th>
        </tr>
      </thead>
      <tr v-bind:key="stock.name" v-for="stock in stocks">
        <td>{{stock.symbol}}</td>

        <td v-if="stock.errMsg" class="errorMsg">{{stock.errMsg}}</td>
        <td v-if="stock.isLoading">Loading..</td>

        <td v-if="showStock(stock)">$ {{stock.initialSharePrice}}</td>
        <td v-if="showStock(stock)">$ {{stock.finalSharePrice}}</td>
        <td
          v-if="showStock(stock)"
        >$ {{Math.round((stock.finalSharePrice - stock.initialSharePrice) * 100) / 100}}</td>
        <td v-if="showStock(stock)">% {{percentageChange(stock)}}</td>
        <td v-on:click="deleter(stock)" id="deleteButton">x</td>
      </tr>
    </table>
    <div id="rightBox">
      <DateRangePicker
        v-bind:intialDateUpdater="initialDateUpdater"
        v-bind:finalDateUpdater="finalDateUpdater"
      />
      <StockSelector :submitStock="submitStock" />
    </div>
  </div>
</template>

<script>
import DateRangePicker from "../control-panel/date-range-selector/DateRangeSelector.vue";
import StockSelector from "../control-panel/stock-selector/StockSelector.vue";

export default {
  name: "StockPicker",
  props: {
    stocks: Array,
    dates: Object,
    updater: Function,
    deleter: Function,
    initialDateUpdater: Function,
    finalDateUpdater: Function
  },
  components: {
    StockSelector,
    DateRangePicker
  },
  methods: {
    showStock: function(stock) {
      if (!stock.errMsg & !stock.isLoading) {
        return true;
      }
      return false;
    },
    submitStock: function() {
      const symbol = document
        .getElementById("stockInputField")
        .value.toUpperCase();
      document.getElementById("stockInputField").value =
        symbol == "SEARCH TICKER SYMBOL." ? "Search ticker symbol" : symbol;

      if (
        symbol &&
        symbol != "SEARCH TICKER SYMBOL." &&
        this.stocks.map(s => s.symbol).indexOf(symbol) == -1
      ) {
        this.updater(symbol);
        document.getElementById("stockInputField").value = "";
      }
    },
    percentageChange: function(stock) {
      const percentage =
        ((stock.finalSharePrice - stock.initialSharePrice) /
          stock.initialSharePrice) *
        100;
      return Math.round(percentage * 100) / 100;
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
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 0;
  height: 22em;
}

#rightBox {
  grid-template-columns: 1fr;
}
table {
  width: 90%;
  border-collapse: collapse;
  border-bottom: 1px solid #454545;
  margin: 1em;
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

input {
  font-size: 1.5em;
  margin: 0rem;
  margin-left: 0.5rem;
  font-weight: 600;
  padding-left: 0.5em;
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
