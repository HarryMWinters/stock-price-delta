<template>
  <nav class="Nav">
    <button class="bio">About The Author</button>
    <a
      class="profesionalLink"
      href="https://www.linkedin.com/in/code-bio/"
      rel="noopener noreferrer"
      target="_blank"
    >
      <img src="@/assets/linkedIn_logo_dark.png" />
    </a>
    <a
      class="profesionalLink"
      href="https://github.com/HarryMWinters"
      rel="noopener noreferrer"
      target="_blank"
    >
      <img src="@/assets/github_logo.png" />
    </a>
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
  background-color: #eeeeee;
  border: 0;
}

.Nav {
  display: flex;
  flex-direction: row;
  padding: 0;
  width: 100%;
  height: 3em;
}

.profesionalLink {
  align-self: flex-end;
  margin: 0.5rem;
  padding: 0.5rem;
  height: 1.5rem;
  width: 10%;
  min-width: 4rem;
}

.bio {
  align-self: flex-start;
  background: rgba(0, 0, 0, 0.755);
  color: var(--eggshell);
  align-self: flex-end;
  margin: 0em;
  padding: 0em;
  margin-right: auto;
  height: 100%;
  padding: 0;
  width: 20%;
  min-width: 12rem;
  font-weight: bolder;
  font-size: 1em;
}

img {
  height: 2rem;
  border-radius: 0.75em;
}
</style>
