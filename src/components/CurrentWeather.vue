<template>
  <section class="container">
    <p class="date">{{ getCurrentDate(weather.current.dt) }}</p>
    <p>Current Weather Conditions in Malta</p>

    <div class="flex-container">
      <div class="svg">
        <WeatherIcon :currentWeather="weather.current.weather[0].description" />
      </div>
    </div>
  </section>
</template>

<script>
import { getCurrentDate } from "../utils";
import WeatherIcon from "../components/WeatherIcon";

export default {
  name: "CurrentWeather",
  props: {
    weather: Object,
  },
  methods: {
    getCurrentDate,
  },

  components: { WeatherIcon },
};
</script>

<style scoped>
.container {
  background-color: rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  width: 100%;
  max-width: 1024px;
  margin: 0 auto;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.date {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.svg {
  width: 15rem;
  padding: 1rem;
}
</style>
