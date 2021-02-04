<template>
  <div id="app">
    <MainScreen />
  </div>
</template>

<script>
import MainScreen from "./views/MainScreen";

export default {
  name: "App",
  components: {
    MainScreen,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
