<template>
  <nav class="Nav">
    <Bio />
    <a
      class="profesionalLink"
      href="https://www.linkedin.com/in/code-bio/"
      rel="noopener noreferrer"
      target="_blank"
    >Linkedin</a>
    <a
      class="profesionalLink"
      href="https://github.com/HarryMWinters"
      rel="noopener noreferrer"
      target="_blank"
    >Github</a>
    <h3>I'm a Nav</h3>
  </nav>
</template>

<script>
export default {
  name: "Nav",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  padding: 0;
  margin: 0;
  width: 100%;
  background-color: #e6f7ff;
}
</style>
