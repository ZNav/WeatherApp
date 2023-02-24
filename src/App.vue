<template>
  <body background-size=cover>
    <WeatherInformation />
  </body>
</template>

<script>
import WeatherInformation from "./components/WeatherInformation.vue";
export default {
  name: "App",
  components: {
    WeatherInformation,
  },
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

html, body {
    margin: 0;
    height: 100%;
    background-color: rgb(129, 129, 219);
}

</style>
