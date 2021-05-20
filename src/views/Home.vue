<template>
  <div class="site-container">
    <CurrentWeather v-if="!loading" :weather="weatherData" />
    <Forecast v-if="!loading" :weather="weatherData.daily.slice(1)" />
  </div>
</template>

<script>
import CurrentWeather from "../components/CurrentWeather";
import Forecast from "../components/Forecast";

export default {
  name: "Home",
  components: {
    CurrentWeather,
    Forecast,
  },

  data() {
    return {
      weatherData: {},
      loading: true,
    };
  },

  methods: {
    // Fetch weather data from the api
    async fetchWeather() {
      const res = await fetch(
        `https://api.openweathermap.org/data/2.5/onecall?lat=35.8997&lon=14.5147&units=metric&exclude=minutely,hourly&appid=${process.env.VUE_APP_APIKEY}`
      );
      const data = await res.json();
      return data;
    },
  },

  async created() {
    const data = await this.fetchWeather();
    this.weatherData = data;
    this.loading = false;
  },
};
</script>

<style scoped>
.site-container {
  min-height: 100vh;
  background-image: url("../assets/bg.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-attachment: fixed;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

@media (min-width: 768px) {
  .site-container {
    background-image: url("../assets/bg-lg.jpg");
  }
}
</style>
