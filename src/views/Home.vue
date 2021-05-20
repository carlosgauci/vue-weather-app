<template>
  <h1>Home</h1>
</template>

<script>
export default {
  name: "Home",

  data() {
    return {
      weatherData: {},
    };
  },

  methods: {
    // Fetch weather data from the api
    async fetchWeather() {
      const res = await fetch(
        `https://api.openweathermap.org/data/2.5/onecall?lat=35.8997&lon=14.5147&units=metric&exclude=minutely,hourly&appid=${process.env.VUE_APP_APIKEY}`
      );
      const data = await res.json();
      this.weatherData = data;
      console.log(this.weatherData);
    },
  },

  async created() {
    this.weatherData = await this.fetchWeather();
  },
};
</script>
