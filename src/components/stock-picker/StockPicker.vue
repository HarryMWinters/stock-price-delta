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
        <td>{{stock.initialSharePrice}}</td>
        <td>{{stock.initialSharePrice}}</td>
      </tr>
    </table>
    <div id="newStock">
      <button>
        <img src="@/assets/add.png" />
      </button>
      <input type="text" value="Search ticker symbol." />
    </div>
  </div>
</template>

<script>
export default {
  name: "StockPicker",
  props: {
    stocks: Array
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.StockPicker {
  background: #bcffde;
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
  background: inherit;
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
  height: 4em;
  margin: 0rem;
  margin-left: 0.5rem;
  font-weight: 600;
  padding: 0.2em;
  padding-left: 0.5em;
  border: 3px solid #454545;
}

#newStock {
  margin: 1em;
  display: flex;
  flex-direction: row;
  width: 60%;
}
</style>
