<template>
  <nav class="myNavbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <img class="navbar-item" src="@/assets/bar-graph-with-dollar-sign.svg" />
      <div class="navbar-item">
        <h1>Stock Analyzer</h1>
      </div>
      <a class="navbar-item" @click="toggleIntro">
        About
        <img src="@/assets/subject.svg" class="mycon" />
      </a>
      <a
        class="navbar-item"
        href="https://github.com/HarryMWinters"
        rel="noopener noreferrer"
        target="_blank"
      >
        Github
        <img src="@/assets/link.svg" class="mycon" />
      </a>
      <a
        class="navbar-item"
        href="https://www.linkedin.com/in/code-bio/"
        rel="noopener noreferrer"
        target="_blank"
      >
        LinkedIn
        <img src="@/assets/link.svg" class="mycon" />
      </a>
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

.mycon {
  height: 30%;
  margin: 0.2em;
}
</style>
