<template>
  <button class="Bio"></button>
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
.Nav {
  display: flex;
  flex-direction: row;
}

.profesionalLink {
  align-self: flex-end;
}
</style>
