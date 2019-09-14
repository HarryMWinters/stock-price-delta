<template>
  <section>
    <label :style="labelStyle">Select a date range...</label>
    <b-field>
      <b-datepicker
        placeholder="Click to select..."
        v-model="dates"
        :style="datePickerStyle"
        @input="updateDates"
        range
      ></b-datepicker>
    </b-field>
  </section>
</template>

<script>
export default {
  name: "DateRangePicker",
  props: {
    intialDateUpdater: Function,
    finaldateUpdater: Function
  },
  data() {
    return {
      datePickerStyle: {
        marginTop: "0em"
      },
      labelStyle: {
        borderBottom: "1px solid #454545",
        fontWeight: "bolder",
        marginBottom: "0.5em",
        padding: "0.4rem 0rem",
        width: "100%"
      },
      dates: []
      // [startDate, endDate]
    };
  },
  methods: {
    updateDates() {
      this.intialDateUpdater(this.dates[0]);
      this.finaldateUpdater(this.dates[1]);
    }
  }
};
</script>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  margin: 1em;
  margin-top: 1em;
  width: 90%;
  padding: 0;
}
</style>
