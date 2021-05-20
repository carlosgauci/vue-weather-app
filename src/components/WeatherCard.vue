<template>
  <div class="container">
    <!-- Day & Date -->
    <h3 class="day">{{ getCurrentDate(day.dt, "array")[0] }}</h3>
    <p class="month">{{ getCurrentDate(day.dt, "array")[1] }}</p>

    <!-- Weather Icon -->
    <div class="svg"><WeatherIcon :currentWeather="day.weather[0].main" /></div>

    <!-- Weather Description -->
    <p>
      {{
        getWeatherConditions(day.weather[0].main, day.weather[0].description)
      }}
    </p>

    <!-- Extra Info -->
    <p>High {{ Math.round(day.temp.max) }}°C</p>
    <p>Low {{ Math.round(day.temp.min) }}°C</p>
    <p>UV {{ Math.round(day.uvi) }}</p>
    <p>{{ getWind(day.wind_deg, day.wind_speed) }} kts</p>
  </div>
</template>

<script>
import { getCurrentDate, getWeatherConditions, getWind } from "../utils";
import WeatherIcon from "./WeatherIcon";

export default {
  name: "WeatherCard",
  props: {
    day: Object,
  },
  components: {
    WeatherIcon,
  },
  methods: {
    getCurrentDate,
    getWeatherConditions,
    getWind,
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem 0;
  flex-basis: 100%;
  position: relative;
}

.day {
  font-size: 1.5rem;
  margin-bottom: 0.1rem;
}

.month {
  margin-bottom: 0.25rem;
}

.svg {
  width: 100%;
  max-width: 5rem;
  margin: 0.75rem 0;
}

.text {
  font-size: 1rem;
  margin-bottom: 0.35rem;
}

@media (min-width: 480px) {
  .container {
    flex-basis: 50%;
  }
}

@media (min-width: 768px) {
  .container {
    flex-basis: 33.3%;
  }
}

@media (min-width: 1024px) {
  .container {
    flex-basis: 25%;
  }
}

@media (min-width: 1280px) {
  .container {
    flex-basis: 14.2%;
  }
}
</style>
