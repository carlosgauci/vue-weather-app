<template>
  <section class="forecast-container">
    <h2 class="title">7 Day Forecast</h2>
    <div class="card-container">
      <WeatherCard v-for="day in weather" :key="day.dt" :day="day" />
    </div>
  </section>
</template>

<script>
import WeatherCard from "./WeatherCard";

export default {
  name: "Forecast",
  components: { WeatherCard },
  props: {
    weather: Array,
  },
};
</script>

<style scoped>
.forecast-container {
  background-color: rgba(0, 0, 0, 0.75);
  border-radius: 10px;
  width: 100%;
  max-width: 1440px;
  margin: 2rem auto 0;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 2rem;
}

.title {
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

.card-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%;
}

@media (min-width: 1024px) {
  .title {
    font-size: 2.5rem;
  }
}
</style>
