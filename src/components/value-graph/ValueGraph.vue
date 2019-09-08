<template>
  <div class="ValueGraph">
    <h3>I'm a Value Graph</h3>
  </div>
</template>

<script>
export default {
  name: "ValueGraph",
  props: {
    // large: Boolean
  }
};
</script>

<style scoped>
.ValueGraph {
  background: var(--bg-element);
  border: 1px var(--border) solid;
  padding: 0;
  margin: 1rem;
  height: 10em;
}

.large {
  margin: 1rem;
  height: 17em;
}
</style>
