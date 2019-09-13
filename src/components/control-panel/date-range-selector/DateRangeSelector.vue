<template>
  <v-date-picker :style="style" attributes="attrs" mode="range" v-model="selectedDate" show-caps />
</template>

<script>
export default {
  name: "DateRangeSelector",
  data() {
    return {
      attrs: [{}],
      style: { padding: "1em" }
    };
  }
};
</script>

<style scoped>
</style>
