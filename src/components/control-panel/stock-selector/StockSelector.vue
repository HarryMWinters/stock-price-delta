<template>
  <div id="newStock">
    <label>Search ticker symbol...</label>
    <input
      type="text"
      id="stockInputField"
      v-on:focus="clearInput"
      v-on:keydown.enter="submitStock"
    />
  </div>
</template>

<script>
export default {
  name: "StockSelector",
  props: {
    submitStock: Function
  },
  methods: {
    clearInput: function(event) {
      if (event.srcElement.value == event.srcElement.defaultValue) {
        event.srcElement.value = "";
      }
    }
  }
};
</script>

<style scoped>
#newStock {
  display: flex;
  flex-direction: column;
  margin: 1em;
  margin-top: 1em;
  width: 90%;
  padding: 0;
}

label {
  border-bottom: 1px solid #454545;
  font-weight: bolder;
  margin-bottom: 0.5rem;
  padding: 0.4rem 0rem;
}

input {
  font-size: 1.5em;
  margin: 0rem;
  margin-left: 0rem;
  font-weight: 600;
  padding-left: 0.5em;
}
</style>