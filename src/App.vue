<template>
  <div id="app">
    <DashBoard msg="Hello Vue in CodeSandbox!" />
  </div>
</template>

<script>
import DashBoard from "./components/DashBoard";

export default {
  name: "App",
  components: {
    DashBoard,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
