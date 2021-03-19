<template>
  <div id="app">
    <trivia-game />
  </div>
</template>

<script>
import TriviaGame from "./components/TriviaGame";
export default {
  name: "App",
  components: {
    TriviaGame
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

