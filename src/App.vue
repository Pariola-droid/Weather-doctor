<template>
  <!-- <div
    id="app"
    :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''"
  > -->
  <WeatherC />
  <!-- </div> -->
</template>

<script>
import WeatherC from "./components/WeatherC.vue";

export default {
  name: "App",
  components: {
    WeatherC,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Dosis:wght@400;500;600&family=Josefin+Sans:wght@300;400&family=Poppins:wght@300;400;500&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
}

#app {
  font-family: "Dosis", sans-serif;
  /*  font-family: 'Josefin Sans', sans-serif;
    font-family: 'Poppins', sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-image: url("./assets/img/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  overflow: hidden;
  height: auto;
  width: 100%;
}

#app.warm {
  background-image: url("./assets/img/warm-bg.jpg");
}

@media only screen and (min-width: 750px) {
  #app {
    background-position: center;
  }
}
</style>
