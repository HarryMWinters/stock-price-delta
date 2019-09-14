<template>
  <section>
    <b-field label="Select a date range...">
      <b-datepicker
        placeholder="Click to select..."
        v-model="dates"
        :style="style"
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
      showWeekNumber: false,
      style: {
        width: "20em"
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
  margin: 1em;
}
b-datepicker {
  width: 2em;
}
</style>
