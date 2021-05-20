<template>
  <CurrentWeather v-if="!loading" :weather="weatherData" />
</template>

<script>
import CurrentWeather from "../components/CurrentWeather";

export default {
  name: "Home",
  components: {
    CurrentWeather,
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
      console.log(data);
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
