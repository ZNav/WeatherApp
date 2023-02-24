<template>
  <div class="container">
    <div class="inner-container">
      <h1 style="margin-top: 20px;">{{ city }}</h1>
      <h2>{{ temperature }}<span>&#176;</span></h2>
      <p>{{ weatherDescription }}</p>
      <div v-if="showClearDay" class="weather-condition">
        <img src="../assets/01d.png" alt="" />
      </div>
      <div v-if="showClearNight" class="weather-condition">
        <img src="../assets/01n.png" alt="" />
      </div>
      <div v-if="showBrokenClouds" class="weather-condition">
        <img src="../assets/04d.png" alt="" />
      </div>
      <div v-if="showFewCloudsDay" class="weather-condition">
        <img src="../assets/02d.png" alt="" />
      </div>
      <div v-if="showFewCloudsNight" class="weather-condition">
        <img src="../assets/02n.png" alt="" />
      </div>
      <div v-if="showMist" class="weather-condition">
        <img src="../assets/50d.png" alt="" />
      </div>
      <div v-if="showRainDay" class="weather-condition">
        <img src="../assets/10d.png" alt="" />
      </div>
      <div v-if="showRainNight" class="weather-condition">
        <img src="../assets/10n.png" alt="" />
      </div>
      <div v-if="showScatteredClouds" class="weather-condition">
        <img src="../assets/03d.png" alt="" />
      </div>
      <div v-if="showSnow" class="weather-condition">
        <img src="../assets/13d.png" alt="" />
      </div>
      <div v-if="showThunderstorm" class="weather-condition">
        <img src="../assets/11d.png" alt="" />
      </div>
      <div v-if="showShowerRain" class="weather-condition">
        <img src="../assets/09d.png" alt="" />
      </div>
      <div class="input-container">
        <label for="latitude">Latitude</label>
        <input
          style="margin: 2px"
          type="text"
          name="latitude"
          v-model="latitude"
        />
      </div>
      <div class="input-container">
        <label for="latitude">Longitude</label>
        <input
          style="margin: 2px"
          type="text"
          name="longitude"
          v-model="longitude"
        />
      </div>
      <button style="margin: 10px" @click="GetWeatherData()">Get Data</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      weather: {},
      weatherDescription: "",
      showClearDay: false,
      showClearNight: false,
      showBrokenClouds: false,
      showFewCloudsDay: false,
      showFewCloudsNight: false,
      showMist: false,
      showRainDay: false,
      showRainNight: false,
      showScatteredClouds: false,
      showSnow: false,
      showThunderstorm: false,
      showShowerRain: false,
      temperature: "",
      city: "",
      latitude: "28.14618",
      longitude: "-82.7568",
    };
  },
  methods: {
    GetWeatherData() {
      this.showClearDay = false;
      this.showClearNight = false;
      this.showBrokenClouds = false;
      this.showFewCloudsDay = false;
      this.showFewCloudsNight = false;
      this.showMist = false;
      this.showRainDay = false;
      this.showRainNight = false;
      this.showScatteredClouds = false;
      this.showSnow = false;
      this.showThunderstorm = false;
      this.showShowerRain = false;
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/weather?lat=" +
            this.latitude +
            "&lon=" +
            this.longitude +
            "&units=imperial&appid=ac8f0d63249133e154516ba4383ddf7c"
        )
        .then((response) => {
          this.city = response.data.name;
          let icon = response.data.weather[0].icon;
          let descriptionString = response.data.weather[0].description;
          this.weatherDescription =
            descriptionString.charAt(0).toUpperCase() +
            descriptionString.slice(1);
          this.temperature = response.data.main.temp;

          if (icon == "01d") {
            this.showClearDay = true;
          }
          if (icon == "01n") {
            this.showClearNight = true;
          }
          if (icon == "02d") {
            this.showFewCloudsDay = true;
          }
          if (icon == "02n") {
            this.showFewCloudsNight = true;
          }
          if (icon == "03d" || icon == "03n") {
            this.showScatteredClouds = true;
          }
          if (icon == "04d" || icon == "04n") {
            this.showBrokenClouds = true;
          }
          if (icon == "09d" || icon == "09n") {
            this.showShowerRain = true;
          }
          if (icon == "10d") {
            this.showRainDay = true;
          }
          if (icon == "10n") {
            this.showRainNight = true;
          }
          if (icon == "11d" || icon == "11n") {
            this.showThunderstorm = true;
          }
          if (icon == "13d" || icon == "13n") {
            this.showSnow = true;
          }
          if (icon == "50d" || icon == "50n") {
            this.showSnow = true;
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.GetWeatherData();
  },
};
</script>

<style>
.container {
  size: cover;
  justify-content: center;
}

.inner-container {
  justify-content: center;
  width: 100%;
  height: 100%;
  background-color: rgb(129, 129, 219);
}
</style>
