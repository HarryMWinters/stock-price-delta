<template>
  <div class="StockPicker">
    <h1>{{ msg }}</h1>
    <h3>I'm a stock picker</h3>
  </div>
</template>

<script>
export default {
  name: "StockPicker",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.StockPicker {
  background: #999;
  margin: 1rem;
}
</style>
