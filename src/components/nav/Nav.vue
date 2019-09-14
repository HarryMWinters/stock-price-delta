<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <img class="navbar-item" src="@/assets/bar-graph-with-dollar-sign.svg" />
      <div class="navbar-item">
        <h1>Stock Analyzer</h1>
      </div>
    </div>

    <div class="navbar-menu">
      <div class="navbar-start">
        <a class="navbar-item" @click="toggleIntro">About</a>
        <a
          class="navbar-item"
          href="https://github.com/HarryMWinters"
          rel="noopener noreferrer"
          target="_blank"
        >Github</a>
        <a
          class="navbar-item"
          href="https://www.linkedin.com/in/code-bio/"
          rel="noopener noreferrer"
          target="_blank"
        >LinkedIn</a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Nav",
  props: {
    toggleIntro: Function
  }
};
</script>

<style scoped>
* {
  background-color: #eeeeee;
  border: 0;
  margin: 0;
}

h1 {
  font-weight: 900;
}

#introText {
  background-color: inherit;
}
</style>
