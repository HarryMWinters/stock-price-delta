<template>
  <div class="ValueReadout">
    <h3>I'm a value readout.</h3>
  </div>
</template>

<script>
export default {
  name: "ValueReadout",
  props: {},
  components: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ValueReadout {
  background: var(--bg-element);
  border: 1px var(--border) solid;
  padding: 0;
  margin: 1rem;
  height: 10em;
}
</style>