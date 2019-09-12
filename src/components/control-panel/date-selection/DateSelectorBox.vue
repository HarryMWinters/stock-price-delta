<template>
  <div id="dateSelectionBox">
    <div id="startBox">
      <h3>Pick Start Date</h3>
      <Datepicker
        placeholder="Select Start Date"
        :disabled-dates="this.initialDisabledDates"
        input-class="{foo}"
      />
    </div>
    <div id="endBox">
      <h3>Pick End Date</h3>
      <Datepicker
        placeholder="Select End Date"
        id="finalSelector"
        :disabled-dates="this.finalDisabledDates"
      />
    </div>
    <!-- <button id="bar">FOO</button> -->
  </div>
</template>

<script>
import Datepicker from "vuejs-datepicker";

export default {
  name: "DateSelectionBox",
  components: {
    Datepicker,
    Datepicker
  },
  props: {
    intialDateUpdater: Function,
    finaldateUpdater: Function
  },
  data() {
    return {
      initialDisabledDates: {
        to: new Date(1999, 1, 1),
        from: new Date()
      },

      finalDisabledDates: {
        from: new Date()
      },

      calendarClass: {
        color: "red"
      }
    };
  }
};
</script>

<style scoped>
#dateSelectionBox {
  padding: 1rem;
  margin: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

#startBox,
#endBox {
  background: #f2f2f2;
  border: 1px solid #ddd;
  padding: 0em 1em 1em;
  margin-bottom: 2em;
  width: 50%;
}
</style>
